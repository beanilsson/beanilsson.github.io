# How difficult can it be to export a pdf?
As it turns out, pretty bloody difficult ...

## Background
I have recently lost my job and to be able to get my share of the unemployment fund, I need to provide evidence that I've worked during the last twelve months, up until the point where I was sacked. Which I think is fair enough. This is done by submitting a verification document provided by the company(ies) where I've been employed during this period of time. Still, fair enough. However, for some reason my unemployment fund want an appendix submitted in a different form than the rest of the verification document, and as I received my verification document as one single pdf, this is where the issues begin.

## Searching for a solution
I started by optimistically opening my then ancient and outdated version of Adobe Acrobat thinking I could just print the pages to images and be done with it. Nope, didn't work. "Could not print file" (or something similar) it said. Well ok, so I turned to the mighty Internet as I had done before on similar occassions. The search phrase "pdf to image converter" generates about 233 000 000 results on G*ogle, DuckDuckGo doesn't show a counter of the number of results, but I guess there are quite a few finds there as well. Sweet! I just needed to upload the file through a form on basically any of these sites and be done with it. But then I stopped myself thinking, "Hold your horses, do you really want to upload documents containing sensitive information like your social security number, to a random website on the interwebz?" And because I am a sensible person, most of the time anyway, I thought "No, I don't. Why should I provide them with my data?" (Although all of our most sensitive data and secrets are probably already wide spread all over the place by now ... *cough* [1177](https://medium.com/@rikardhjort/2-7-medical-calls-breached-in-sweden-and-its-pure-comedy-b93c1af95e06)*cough*)

Anyway, I thought I would be better off with a native (Windows) app instead, and I probably would have if I had been able to find one suiting my needs. I upgraded Adobe Acrobat and found that there was an export option. Hallelujah! Praise the Gods! But no, the only formats I could export this by now, godforsaken, pdf to were `.docx, .doc, .rtf, .xlsx and .pptx`. Really? Ok, I don't know how strong of a usecase it is to export pdf pages to images, but come on, why not have it as an option? But no, let's have `.rtf` as an option, it was updated 2008 after all ... Disclaimer, I'm not an expert on text file formats so `.rtf` might be the cream of the crop and I'm just talking out of my ass.

(I also tried opening the file in OpenOffice Draw, which was a horrible mistake.)

As the applications I already had installed had failed me I decided to program something myself. There are lots of handy `node packages` and `ruby gems` you can use and not much more code is required, ten lines of code tops should suffice. But, being on Windows there is always something else to rain on your parade. In this case it's called `ImageMagick`, alright I'm being a bit unfair and I'm sure it's a great tool, but it is a serious, horrendous pain to get working ... I wanted to use the `RMagick` gem to convert my pdf. This gem require, of course, `ImageMagick`. If you're interested, there's quite a nice guide [here](https://medium.com/ruby-on-rails-web-application-development/install-rmagick-gem-on-windows-7-8-10-imagemagick-6-9-4-q16-hdri-5492c3fef202) on how to set it up. You can't use `ImageMagick` 7+ though, and if you've used RubyInstaller2 you need to copy all of the `ImageMagick` core files to `RubyInstaller2` root.

At this point I felt that the programming project was starting to grow into some sort of gooey mess which would take much more time to finish than I felt spending on it, so I abandoned it.

## At last!

Continuing on my journey I turned to Internet once again to find some software to download instead. I didn't want to download any piece of code so I chose to go down the path of open source (of course, duh), and settled for [PDFedit](http://pdfedit.cz/en/index.html) which while it worked nicely, it was just as useless as Acrobat at exporting the pages separately. It had an interesting feature though, "Snapshot" they called it, which allows the user to take snapshots of the page. For some reason I couldn't use this tool on my specific pdf, but I finally had a solution!

Once again I opened the file in Acrobat, whipped out GreenShot and took screen shots of each page and saved them as individual pages, uploaded the pages to the unemployment fund, done.

## Afterthoughts

In retrospect it feels like I should have thought of this solution from the beginning. It is by far the most simple and quickest way to achieve what I wanted. But at the same time I sort of expect a pdf tool to be able to twist and turn and edit the files in any way I want it to. Is it too much to expect a file editing tool to be able to export the file in more than five different formats? I don't think so.
