

# How change text to speech


## Change .pdf file to text if you need.
```
pdftotext -layout file_name.pdf output.txt
```

## Install espeak or espeak-ng

## List all available voice languages
```
espeak --voices
```

I chose the Polish language, so I used option
```
-v polish
```

## Reading text file 
```
espeak -v polish --stdout -f file_name.txt | aplay
```

## Change text file to .mp3
```
espeak-ng  -v polish --stdout -f file_name.txt | ffmpeg -i - -ar 44100 -ac 2 -ab 192k -f mp3 output.mp3
```

You can also read blog <https://nealgodfrey.com/how-to-convert-text-document-to-speech-on-ubuntu-using-espeak/>  
which helped me. Thank you! :-)

## Example script
https://github.com/tele1/LinuxScripts/blob/main/change.pdf.to.mp3.sh