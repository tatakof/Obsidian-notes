### Base64 
In [computer programming](https://en.wikipedia.org/wiki/Computer_programming "Computer programming"), **Base64** is a group of [binary-to-text encoding](https://en.wikipedia.org/wiki/Binary-to-text_encoding "Binary-to-text encoding") schemes that represent [binary data](https://en.wikipedia.org/wiki/Binary_data "Binary data") (more specifically, a sequence of 8-bit bytes) in sequences of 24 bits that can be represented by four 6-bit Base64 digits.

Common to all binary-to-text encoding schemes, Base64 is designed to carry data stored in binary formats across channels that only reliably support text content. Base64 is particularly prevalent on the [World Wide Web](https://en.wikipedia.org/wiki/World_Wide_Web "World Wide Web")[[1]](https://en.wikipedia.org/wiki/Base64#cite_note-1) where one of its uses is the ability to embed [image files](https://en.wikipedia.org/wiki/Image_files "Image files") or other binary assets inside textual assets such as [HTML](https://en.wikipedia.org/wiki/HTML "HTML") and [CSS](https://en.wikipedia.org/wiki/CSS "CSS") files.[[2]](https://en.wikipedia.org/wiki/Base64#cite_note-2)

Base64 is also widely used for sending e-mail attachments. This is required because [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol "Simple Mail Transfer Protocol") – in its original form – was designed to transport 7-bit ASCII characters only. This encoding causes an overhead of 33–37% (33% by the encoding itself; up to 4% more by the inserted line breaks).


### ROT13
**ROT13** ("**rotate by 13 places**", sometimes hyphenated **ROT-13**) is a simple letter [substitution cipher](https://en.wikipedia.org/wiki/Substitution_cipher "Substitution cipher") that replaces a letter with the 13th letter after it in the alphabet. ROT13 is a special case of the [Caesar cipher](https://en.wikipedia.org/wiki/Caesar_cipher "Caesar cipher").

Because there are 26 letters (2×13) in the [basic Latin alphabet](https://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet "ISO basic Latin alphabet"), ROT13 is its own [inverse](https://en.wikipedia.org/wiki/Inverse_function "Inverse function"); that is, to undo ROT13, the same [algorithm](https://en.wikipedia.org/wiki/Algorithm "Algorithm") is applied, so the same action can be used for encoding and decoding. The algorithm provides virtually no [cryptographic](https://en.wikipedia.org/wiki/Cryptography "Cryptography") security, and is often cited as a canonical example of weak encryption

### Hex dump
In computing, a hex dump is a hexadecimal view (on screen or paper) of computer data, from memory or from a computer file or storage device. Looking at a hex dump of data is usually done in the context of either debugging, reverse engineering or digital forensics.[1]

In a hex dump, each byte (8 bits) is represented as a two-digit hexadecimal number. Hex dumps are commonly organized into rows of 8 or 16 bytes, sometimes separated by whitespaces. Some hex dumps have the hexadecimal memory address at the beginning.

Some common names for this program function are hexdump, hd, od, xxd and simply dump or even D.

### Public and Private keys
Public key authentication is more secure than password authentication. 
With public key authentication, the authenticating entity has a public key and a private key. Each key is a large number with special mathematical properties. The private key is kept on the computer you log in from, while the public key is stored on the **.ssh/authorized_keys** file on all the computers you want to log in to. When you log in to a computer, the SSH server uses the public key to "lock" messages in a way that can only be "unlocked" by your private key - this means that even the most resourceful attacker can't snoop on, or interfere with, your session. As an extra security measure, most SSH programs store the private key in a passphrase-protected format, so that if your computer is stolen or broken in to, you should have enough time to disable your old public key before they break the passphrase and start using your key. Wikipedia has a [more detailed explanation](http://en.wikipedia.org/wiki/Public-key_cryptography "WikiPedia") of how keys work.
