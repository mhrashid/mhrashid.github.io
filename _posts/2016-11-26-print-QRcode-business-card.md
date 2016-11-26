---
layout: single
title:  "Let's Print Our Own Business Cards"
date:   2016-11-23 00:06:21 +0900
read_time: true
comments: true
share: true
#categories: category1 category2
---
{% include toc %}

<p align="left">
<a href="http://imgur.com/4H9NMJt"><img src="http://i.imgur.com/4H9NMJt.png" title="source: imgur.com" /></a>
</p>

[Photo Credit](http://www.bristolglobal.com/country-profile-japan-assignment-in-the-land-of-the-rising-sun/#.WDlBb7W1nIo)


####  Trend of using QR code   

Using QR codes became a trend among tech users now-a-days. It can be used for pretty much anything a bar code is. However, a QR code accommodates more information than a barcode does and therefore it is widely used. We can scan a QR code and readily make a phone call, send a mail/message without typing the receiver address. QR codes are being distributed to handover discount coupons, Wi-Fi networks, product information, webpage URLs, etc.  

####  Use of QR code in Academia   

Academia also adopted the idea of QR codes for many uses. Poster presenters are putting QR codes to share contact, project URLs, link to related publications. [Here](http://imgur.com/BEaboLi) is a poster that I presented in ISRS Conference 2015. This is definitely a smarter idea because the audience can save those information in their smartphone/tab through a quick scan for further communication or reading. For the same reason QR codes are also printed in the business card. With this idea in mind, I printed my QR code business card a couple of years ago.

####  Preparing of QR code business card    

There are thousands of business card templates out there. You can pick one and modify to fit in your QR code. Any free online QR code generator will make you one. For example, [this site](http://goqr.me/) seems fine to me. Select the type of your code. For business card, probably you would like to select ‘vcard’ option. Plug-in you information and download the image. Viola! Now you are ready to include your QR code in your business card.

####  LaTeX based QR code business card   

For preparing my business card, I took a different approach. Since I am very fond of using LaTeX, I googled and found [this code](https://blog.bramp.net/post/2010/02/13/latex-qr-based-business-card/) for making a QR code based business card. I don’t need to use any third party program or online link to make the QR code! However, I was having hard time to run the code since the package is outdated. Some commenter in this post suggested using an extra package.

```
\usepackage{pst-barcode}
\usepackage{auto-pst-pdf, pst-barcode}
```

Still some extra steps were to follow to compile the code. auto-pst-pdf package will not work until the code is being compiled with –shell –escape enabled. Since I use TeXStudio as my Tex Editor, I made the following changes before compiling.
```
Option ---> Configure TeXstudio ---> Commands ----> PdfLaTeX
```   

This is how I configured TeXstudio to compile the file.

<a href="http://imgur.com/c9xnmdw"><img src="http://i.imgur.com/c9xnmdw.png" title="source: imgur.com" /></a>


Before compiling the Tex file,  the dimension of the card in this LaTeX code (85 x 55, which is [UK standard])(https://en.wikipedia.org/wiki/Business_card) needed to be adjusted to Japan Standard. So I tweaked the dimension to 91 x 55. I also changed the color of the horizontal rules and QR codes to 'gray'.

Finally this is what the preamble of my .tex file looked like

```
\documentclass[11pt,a4paper]{memoir}

\setstocksize{55mm}{91mm} % Japan Stock size
\setpagecc{55mm}{91mm}{*}
\settypeblocksize{48mm}{80mm}{*}
\setulmargins{5mm}{*}{*}
\setlrmargins{5mm}{*}{*}

\setheadfoot{0.1pt}{0.1pt}
\setheaderspaces{1pt}{*}{*}
\checkandfixthelayout[fixed]

\pagestyle{empty}

\usepackage{pstricks}
\usepackage{auto-pst-pdf, pst-barcode}
\usepackage{mathpazo}

%--------------------------------------- %
% change to color of the horizontal rule
%-------------------------------------- %
\makeatletter
\let\old@rule\@rule
\def\@rule[#1]#2#3{\textcolor{rulecolor}{\old@rule[#1]{#2}{#3}}}
\makeatother

\usepackage{xcolor}
\colorlet{rulecolor}{black!50!white}
%-------------------------------------- %

\begin{document}
```   

Finally I could make a single card. Now I can print it in multipage option and split individual cards with cutter/blade. There are some other LaTeX codes for QR code business card which will produce a pdf with multiple cards. But I didn’t like the design. Instead I used PdfTK command line tool in Linux (Ubuntu) to make the multi-card pdf.


####  How to print the business card in multiple pages      

In Japan, there are many business card printing papers available which are very convenient. Once a multi-card pdf is printed on this paper, the individual cards can be split seamlessly since there are splitting lines.

<a href="http://imgur.com/XkG4x0s"><img src="http://i.imgur.com/XkG4x0s.png" title="source: imgur.com" width='500'/></a>


-  Created QR code business card (single page) by latex code (as above).
-  Install two packages in linux through terminal, if you have not yet installed. `PDFtk` and `PDFjam`. These tow packages can be installed from terminal by  

```
sudo apt-get install pdftk', 'sudo apt-get install pdfjam
```   

-  Copy the qrcode.pdf in desktop
-  Change directory in terminal.  

```
cd Desktop
```  

-  Copy qrcode.pdf 10 times in desktop (by copy-pasting) and rename them 1.pdf....10.pdf.
-  In terminal
```   
pdftk 1.pdf 2.pdf 3.pdf 4.pdf 5.pdf 6.pdf 7.pdf 8.pdf 9.pdf 10.pdf cat output merged.pdf
```   

The source for this code is [here](http://superuser.com/questions/366490/how-to-merge-multiple-pdf-files-onto-one-page-with-pdftk).

-  In terminal

```
pdfjam --nup 2x5 --papersize '{8.5in,11in}' --noautoscale true merged.pdf -o 10upcard.pdf
```   

The source for this code is [here](http://askubuntu.com/questions/30962/good-business-card-creation-software).

-  10upcard.pdf is the output pdf. Print it in Japanese business card paper. Set the printer in 'no scaling' and 'Auto center enabled'.

-  I used Foxit PDF Reader since Adobe PDF Reader was not working well. doesn't work good.


Finally I got this! And I am pretty much happy with the outcome.


<a href="http://imgur.com/Wzr8ymI"><img src="http://i.imgur.com/Wzr8ymI.jpg" title="source: imgur.com" width='500'/></a>


Now let's learn some etiquettes of exchanging business cards in Japan from this [nice post](https://blog.gaijinpot.com/exchanging-business-cards-japan/).
