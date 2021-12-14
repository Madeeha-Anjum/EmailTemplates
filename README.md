# Email Templates

This repository includes the basics of coding responsive emails. It will show you how to make an email that is always responsive. Even in a worst-case scenario eg. where CSS support is not available.

**Table of contents**

- Preamble
  - Resources
  - Testing Guide
  - Image hosting
- Getting Started Guide
  - Intro
  - Basics
  - outer-container/Ghost tables
  - Banner/Single Column
  -

## Preamble

#### 1. Resources

- [Getting Started Guide | `Oct 21, 2021`](https://webdesign.tutsplus.com/tutorials/creating-a-future-proof-responsive-email-without-media-queries--cms-23919)

- [Good guide2](https://www.goodemailcode.com/email-code/template.html)

- [Checking suppot](https://www.caniemail.com/features/)

- [Email container](https://www.emailonacid.com/blog/article/email-development/which-code-should-i-include-in-every-email/)

- [good read](https://www.emailonacid.com/blog/article/email-development/email-development-best-practices-2/)

#### 2. Testing site

[Testing](https://www.putsmail.com/tests/new)
Send HTML Emails using this: https://www.thunderbird.net/en-US/

#### 3. Image hosting

<img src="./img/gDriveId.png"
     alt="gDriveId"
     style="float: right; margin-right: 10px; height:200px" />

[Image hosting](Google drive)
[lightshot create QR code](https://www.lightshot.org/en/create-qr-code)

https://drive.google.com/u/0/uc?id=`[insert id]`export=view
id can be found in the url here

## Getting started Guide

**Some rules**

1. Emails have a width of 660px
2. Outlook dose not support max width, margin, display inline block
3.

#### 1. Intro

**Problem**
Email clients will sometimes strip the key portions from the `<head>` which often contains CSS and media queries. Some email clients will send only the `<body>` tag. This tutorial will help you to create a responsive emails keeping these situations in mind.
`For example: Gmail app on your phone allows non gmail accounts but strips the <style> tags`

**Solution**
Method: `Fluid hybrid` approach
Definition: `fluid` refers to using `%` and elements that expand to fill there space. `hybrid` is because we use max-width to constrain the free flowing elements.

1.  ..That it; comes in at a tidy 17kb file size!
2.  This approach ensures that your columns all aligned in the center on mobile even without media queries
3.  This approach ensures that your columns have the ability to vertically align themselves on mobile even without media queries
4.  This approach gives you total control over content blocks that stack and flow

#### 2. Basics

1. We already know what these are: `<!DOCTYPE html>`,`<html..`, `<meta charset=...`, `<meta name="viewport"...`

2. `<meta http-equiv="X-UA-Compatible" content="IE=edge" />` display content in the highest IE mode available. Only useful if the user is using IE8, 9 and 10. It is disabled in IE11 which is the current stable version of IE. So this is up to you to decide if you want to use it or not.But if you do use it you need to add `<!--[if !mso]><!-->` before and `<!--<![endif]-->` after so images in mo are not messed up

3. `<title></title>` it is best to leave the title tag empty since some clients display the title right after the subject line

4. `<!--[if mso]>` and `<![endif]-->` are styles applied only to Microsoft Outlook

5. `border-spacing:0` is used to remove the space between the cells in the table. And `margin:0 !important` for `<div>` tags, otherwise Outlooks add extra space

6. `<o:OfficeDocumentSettings>` tells MO to use base resolution of 96dpi

7. The `<body>` tag has basic styles: margin padding word-space and background.

8. The wrapper `<div>` contains the main content and sets some CSS for text sizing and language. `aria-roledescription="email"` for screen readers to announce the email. And `role="article"` tells screens readers how to interpret.

9. Lastly we include a big wrapper table to help center the main content. We always set the role to presentation.

```html
<!DOCTYPE html>
<html
  lang="en"
  xmlns="https://www.w3.org/1999/xhtml"
  xmlns:o="urn:schemas-microsoft-com:office:office"
>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <meta name="x-apple-disable-message-reformatting" />
    <!--[if !mso]><!-->
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <!--<![endif]-->
    <title></title>
    <!--[if mso]>
      <style type="text/css">
        table {
          border-collapse: collapse;
          border: 0;
          border-spacing: 0;
          margin: 0;
        }
        div,
        td {
          padding: 0;
        }
        div {
          margin: 0 !important;
        }
      </style>
      <noscript>
        <xml>
          <o:OfficeDocumentSettings>
            <o:PixelsPerInch>96</o:PixelsPerInch>
          </o:OfficeDocumentSettings>
        </xml>
      </noscript>
    <![endif]-->
  </head>
  <body
    style="margin:0;padding:0;word-spacing:normal;background-color:#ffffff;"
  >
    <div
      role="article"
      aria-roledescription="email"
      lang="en"
      style="-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%;background-color:#ffffff;"
    >
      <table role="presentation" style="width:100%;border:0;border-spacing:0;">
        <tr>
          <td align="center">[content goes here]</td>
        </tr>
      </table>
    </div>
  </body>
</html>
```

#### 2. Outer Container / Ghost tables

**Problem**
We need to cater separately for Outlook on windows
since will be using `<divs>` that use max-width and display inline block and outlook dose not support these. So we will nest out code inside `[if mos]`

**Solution**
out ghost table will have `width = 660px` and other clients will have a div with`width:96% max-width:660px` meaning we have 2% padding on smaller screens

Note: margin

```html
<!--[if mso]>
<table role="presentation" align="center" style="width:660px;">
<tr>
<td style="padding:20px 0;">
<![endif]-->
<div class="outer" style="width:96%;max-width:660px;margin:20px auto;">
  [content goes here]
</div>
<!--[if mso]>
</td>
</tr>
</table>
<![endif]-->
```

#### 3. Banner / Single Column

At this point we have setup our outer structure.
Now it is time to add some content!!!
