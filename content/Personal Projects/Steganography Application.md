This is a program that I have built and rebuilt over the years. This version is built in python as it is the simplest to package and create an executable for. 

Features:
* Encoding up to 7 bits of RGB data from multiple formats
* Decoding up to 7 bits
* Downloading both encoded or decoded photos
* Bit scrambling

Manipulation Techniques:
* Numpy was used to do the large vectorized matrix math, for faster encoding and decoding speeds
* The bit scramble has a seed that is hard-coded into the program itself, so if the bits are scrambled, only those who own a copy of this software can unscramble it for the image
* The idea was to use MSBs and LSBs to encode one image into another, so many bit manipulation techniques were used

---
[[Download Steganography App for macOS (v1.0.0)]](https://github.com/ImaginationCrab/SteganographyApp/releases/tag/v1.0)

--- 

FAQ:

* What is steganography?
Steganography is the practice of concealing information, in this program you are able to "hide" one image inside of another
* Why do you say built and rebuilt?
I have built this program 3 times, twice in Java and once in python. I built this for the first time at a very early stage of my life, which if you wish to know, you're going to have to ask me yourself.
* What is this useful for?
In cybersecurity, and many other fields which require critical information to be shared but not known, this is used often to pass information around that is also available to the public. Obviously, this program is very simple version of a real steganography program, but still a very interesting project to build, as it involves many techniques that can be applied to other projects.


I will have a video and some photos to showcase the application further.