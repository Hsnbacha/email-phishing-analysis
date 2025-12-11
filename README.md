# Email-phishing-analysis
Analyzed phishing email samples to identify malicious payloads and IoCs, using tools to simulate safe email sandboxing and document findings.
emails one of the most popular methods used by an attacker to achieve initial
 
access specifically using the phishing technique. We are doing CTF for BLue LAB Team: the planet's Prestige.
 
An email was sent to a company and we need to check if this is a suspicious email so we need to do analysis and investigation to check whether this email is suspicious.

To be on a safe side we need to isolate this file and download it. I will be using Virtual box to perform this analysis.

git add images/my_screenshot.png


We can see here the Delivered to 
and the recived by "The email server which is the same as how post office deliver mail and the mail will end up in multiple post office before reaching the post near the recipient

image 2

while here the line 28 Received is the very first received is going to be the mail server that's closest to the sender whereas all the way at the top the first received from the top is going to be closest to the recipient

x appended to the front these are

called X headers and they are optional

and included by tools or mail servers

image 3


and then we have what are called ARC

headers 
Image 4

AKA authenticated received chain

headers these are used for verification

purposes by having a trusted

intermediate email server digitally

signed the header.

Image 5
we

get return path this is the email

address that will be used if the email

fails to send which is typically used

for troubleshooting."where you tried to send an

email but then you got an email failed

to deliver and because you received the

email failed to deliver your email

address was likely put into the return

path"

image 6

authentication results this is where we

can see the statuses for email

protection such as SPF dkim (DomainKeys Identified Mail) and dmarc (Domain-based Message Authentication, Reporting, and Conformance) as

we can see SPF is currently set to fail

meaning that the domain of my micro

Apple 

image 7

 which is this one right here micro

apple.com does not permit the mail

server of 93.99.104.210 as a permitted sender in other

words microappale.com does not know who is 93.99.104.210 is



Through doing the email analysis looking at the

SPF dkim and dmarc statuses is a good

indicator for suspicious emails 
if SPF is set to fail you might want to take a

deeper look into it and then we have the

 "the recipient, subject

and the from" so who sent the email 

image 8


While we are checking we found that Reply-To: 

image 9

email address that is

listed here is what will be used the

moment the recipient clicks on

reply to the email and if you notice the

email has a domain of pashter.com and

then if we look at the from email it is

from microaapple.com because there's a

discrepancy between the two that is

pretty suspicious not only did SPF fail

but the email addresses in the from and

reply to field are different

Image 10 

we

have content type this field is to

instruct the mail server on how to

render the content of the email isit 

being multipart/mixed that means

there are multiple formats 
 it also

has a boundary set for it where the

boundary is bound_600 "a boundary

is used to let the mail server know when

to start and stop rendering the contents

using a certain format"

image 11

message ID which is a unique identifier

to help keep track of this email and

image 12

finally we have the date when the the

recipient received the email we keep

in mind that the date field can be

spoofed


image 13

we then see our first boundary

which will tell the mail server to start

rendering the content using the

following format


image 14-15
if we look at the

content type it says text/plain so it's

telling the mail server" to hey render

this content using plain text format"

at the bottom we see an encoding as well

you want to encode it using Base 64


image 16

the mail server is like sure why not let

me render this using plain text and I'll

encode it using Base 64 and anytime we get

hit with a Base 64 we want to start

decoding it to see the contents of it so we can highlight it and 

then we'll use a

trusty tool called cyberchef 

Image 17

Now we can see the outputs here and it

says "hi the major on Earth the abducted ..."

image 18

we do see

a content type of application/PDF

with the name of puzzletoCOcanca. PDF so

this is going to be the attachment that

was mentioned in the body of the email

we do see the content transfering coding

as base 64 and we do see the base 64

content here so just like previously

I'm actually going to

select two hex and convert this into

hexad decimal now the reason I am doing

this is because if we take a look at the

first couple bytes 

image 19
which is 50 4B 03 04 the first bite of a file makes up

what is called a file signature AKA a

magic number or file header and just

because the file name right here is

called puzzletococada.PDF doesn't

necessarily mean it is a PDF file we

want to always take a look at the file

signature for a file to determine

exactly what that file is now going back

over to cyberchef and copying the first

couple bytes I am going to use a site

called GCK file signature. 

image 20
the first

couple bytes relate to a zip extension

interesting now it did say PDF over to

the file name however if we took a look

at the file signature it has a file

extension of zip what if we did PDF

instead so if I were to just search up

pdf looking at the file extension





