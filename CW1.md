# University of London International Programmes

# Computing and Information Systems/Creative Computing
# CO3326 Computer Security

# Coursework assignment 1 2018-19

__IMPORTANT:__ all students have been allocated a unique set of cipher text and intercepted key stream and seed to use for this coursework assignment. You can obtain this using your Student Reference Number (SRN) from the following URL: http://foley.gold.ac.uk/cw19/api/cw1/{srn}. For example, if your SRN is 877665544, you would obtain your data from http://foley.gold.ac.uk/cw19/api/cw1/877665544. If you have difficulties obtaining your cipher text and intercepted key stream and seed, please email us at: intcomp@gold.ac.uk

This coursework assignment is designed to help you enrich your learning experience and to encourage self-study and creativity. Chapter 5 (pages 49-52) of the subject guide and the suggested supplementary reading will help you in completing this assignment. You should read the coursework assignments carefully and pay particular attention to the [Submission requirements](#submission-requirements).

You are expected to submit __two__ files: a __report__ and a __results sheet__. The _report_ counts as __60%__ of your coursework assignment mark, in which you're expected to answer the questions below. The _results sheet_ counts as __40%__ of your mark, in which you're expected to summarise the results of your calculations in a specific format. Please use the cipher text and keys provided when answering the questions and when compiling the results sheet.

To complete the coursework assignment, it will make your life easier if you write a program. You are welcome to use any programming language. Please include key snippets of your code as an annex at the end of your report.

## Linear Feedback Shift Register

Suppose you are an avid hacker working for a security agency and you are eavesdropping on a converstion between _Alice_ and _Bob_. You intercept a cipher text that you know has been sent from Alice to Bob. You look up both Alice and Bob's public keys in a key directory. You know that they are using an RSA cryptosystem. You assume that Alice wants to be sure that only Bob can decrypt the message. You also assume that Bob wants to be sure that Alice has sent the message. You would like to decrypt the message.

__IMPORTANT:__ To answer the questions below, please use the cipher text and public keys (of Alice and Bob) that you obtained using your SRN.

### Question 1
Describe briefly the steps you need to take to decipher the message.

### Question 2
Which algorithms would be feasible for factorisation for the particular keys that you are trying to break? Compare the algorithms very briefly in terms of:

- number of digits they can deal with,
- time efficiency,
- memory consumption.

### Question 3
Break Alice and Bob's key. State the factorisation algorithm you use and state the running time. If you rely on an online service, state the service you're using and investigate what algorithm is backing the service. _Note_: you will only be able to achieve half marks for this question if you rely on an online tool.

### Question 4
What are the implications of the following assumptions on the keys used?

- Alice wants to be sure that only Bob can decrypt the message,
- Bob wants to be sure that Alice has sent the message.

### Question 5
Are there any restrictions on the ordering of the keys when encrypting? Using your numbers explain why. Is the ordering the same on decryption?

### Question 6
Decipher the message. Show your work.

### Annex
Briefly - in one paragraph - describe the design of your code. Attach key snippets to the annex. Don't forget to acknowledge all sources. Make sure you acknowledge any code re-use.

__REMINDER:__ It is important that your submitted coursework assignment is your own individual work and, for the most part, written in your own words. You must provide appropriate in-text citation for both paraphrase and quotation, with a detailed reference section at the end of your coursework. Copying, plagiarism and unaccredited and wholesale reproduction of material from books or from any online source is unacceptable, and will be penalised (see our [guide on how to avoid plagiarism on the VLE](https://computing.elearning.london.ac.uk/mod/page/view.php?id=5176)).


## Submission requirements

You should upload __two__ single files only.  These must not be placed in a folder, zipped, _etc._

The __report__ should be submitted as a PDF document following a _strict naming scheme_: `YourName_{srn}_CO3326_cw1.pdf`. For example, Steve Jobs with SRN 877665544 would submit `SteveJobs_877665544_CO3326_cw1.pdf`.

The __results sheet__ should be submitted as a JSON file with a _strict format_ and _strict naming scheme_. This summarises the results of your calculations and will be automatically checked by an algorithm, so pay particular attention to its format. The name of the file should be `YourName_{srn}_CO3326_cw1.json`; for example, Steve Jobs with SRN 877665544 would submit `SteveJobs_877665544_CO3326_cw1.json`.

You have obtained the _cipher text_ and the _keys_ in the following format (this is an example for illustration):

```json
{
  "srn": "877665544",
  "name": "Steve Jobs",
  "lfsr": {
    "seed": "11010000101"
  },
  "interception": "10100100001001101001011",
  "cipherText": "a5dc26183f945cbb6732"
}
```

For this _cipher text_ and intercepted _key stream fragment_ and _seed_, Steve Jobs would submit the following JSON, which reflects a correct solution:

```json
{
  "srn": "877665544",
  "name": "Steve Jobs",
  "lfsr": {
    "taps": [
      10,
      8
    ],
    "seed": "11010000101"
  },
  "interception": "10100100001001101001011",
  "key": "d0b24f6e5ae62fd2134b",
  "plainText": "university",
  "cipherText": "a5dc26183f945cbb6732"
}
```

You can use this well-formed JSON to adapt for your numbers and your calculation results.

As the JSON is evaluated by an algorithm, every quote, comma, colon, curly brace upper/lower case is crucial. Please pay attention to these. It would be a shame to lose a potential __40%__ of the total marks for this coursework assignment because of a misplaced comma or a missing quote. There are online tools you can use for JSON formatting and validation (for example [this](https://jsonformatter.curiousconcept.com/)), so double-check that your JSON is syntactically correct.

Please note that the numbers are enclosed within quotes. There is a hint here: the numbers are too large to be represented as `long` or `int`.

### Help

In order to encrypt/decrypt a message, you need to encode the text (string) as a number. If you write your code in `Java`, you can use the following methods:

* for encoding:
```java
 public static BigInteger encode(final String text) {
     return new BigInteger(text, Character.MAX_RADIX);
 }
```
* for decoding:
```java
 public static String decode(final BigInteger number) {
     return number.toString(Character.MAX_RADIX);
 }
```

Alternatively, if you're writing your program in a language other than `Java`, you can rely on the following web service for encoding/decoding:

- http://foley.gold.ac.uk/cw18/api/encode?text=university
- http://foley.gold.ac.uk/cw18/api/decode?number=3113163156336982

obviously replacing `university` or `3113163156336982` in the URL with the text or number you want to encode/decode. The service works for one-word texts (so no space or special characters). There is another hint here: if your decryption is correct, you will get a recognisable English word.
