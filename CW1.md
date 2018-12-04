# University of London International Programmes

# Computing and Information Systems / Creative Computing
# CO3326 Computer Security

# Coursework assignment 1 2018-19

__IMPORTANT:__ all students have been allocated a unique set of cipher text, intercepted key stream fragment and seed to use for this coursework assignment. You can obtain this using your Student Reference Number (SRN) from the following URL: http://foley.gold.ac.uk/cw19/api/cw1/{srn}. For example, if your SRN is 877665544, you would obtain your data from http://foley.gold.ac.uk/cw19/api/cw1/877665544. If you have difficulties obtaining your cipher text, intercepted key stream fragment and seed, please email us at: intcomp@gold.ac.uk

This coursework assignment is designed to help you enrich your learning experience and to encourage self-study and creativity. Chapter 5 (pages 49-62) of the subject guide and the suggested supplementary reading is a good starting point and will help you in completing this assignment. You should read the coursework assignments carefully and pay particular attention to the [Submission requirements](#submission-requirements).

You are expected to submit __two__ files: a __report__ and a __results sheet__. The _report_ counts as __60%__ of your coursework assignment mark, in which you're expected to answer the questions below. The _results sheet_ counts as __40%__ of your mark, in which you're expected to summarise the results of your calculations in a specific format. Please use the cipher text and keys provided when answering the questions and when compiling the results sheet.

To complete the coursework assignment, it will make your life easier if you write a program. You are welcome to use any programming language. Please include key snippets of your code as an annex at the end of your report.

## Linear Feedback Shift Register

A _linear feedback shift register_ is a register of bits that performs discrete step operations that:

- Shift all of the bits one position to the left and
- Replaces the vacated bit by the _exclusive or_ (XOR) of certain bits shifted off, indicated by the _tap_ positions.

A LFSR has three parameters that characterize the sequence of bits it produces: the number of bits _N_, the initial _seed_ (the sequence of bits that initializes the register), and the the tap positions _tap_. The following picture illustrates one step of an 11-bit LFSR with initial seed 11010000101 and tap positions 10 and 8.

![One step of an 11-bit LFSR with initial seed 11010000101 and tap positions at bits 10 and 8](https://raw.githubusercontent.com/vilmosz/cw19/master/LFSR.png)

Please do some research around LFSRs, starting from your subject guide (Chapter 5), suggested readings and W
[Wikipedia](https://en.wikipedia.org/wiki/Linear-feedback_shift_register). Make sure you also understand the [Berlekamp-Massey algorithm](https://en.wikipedia.org/wiki/Berlekamp%E2%80%93Massey_algorithm) as it will be necessary for you to complete the coursework.
 
In your research and reading you'll find references to _polynomials_ in the context of LFSRs, for example _x^11 + x^9 + 1_, which is equivalent to _tap positions_ 10 and 8 and incidentally is a maximal length polynomial / tap positions for an 11-bit LFSR, allowing a maximum period of _2047 = 2^11 - 1_.

## Assignment

Suppose you are an avid hacker working for a security agency and you are eavesdropping on a conversation between _Alice_ and _Bob_. You intercept a _cipher text_, a _key stream fragment_ and a _seed_ that you know has been sent from Alice to Bob. You know that they are using an cryptosystem based on LFSRs. You would like to decrypt the message.

__IMPORTANT:__ To answer the questions below, please use the _cipher text_, intercepted _key stream fragment_ and _seed_ that you obtained using your SRN.

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

## Example

You have obtained the _cipher text_, intercepted _key stream fragment_ and _seed_ in the following format (this is an example for illustration):

```json
{
  "srn": "877665544",
  "name": "Steve Jobs",
  "lfsr": {
    "seed": "11010000101"
  },
  "keyFragment": "10100100001001101001011",
  "cipherText": "a5dc26183f945cbb6732"
}
```

For this _cipher text_, intercepted _key stream fragment_ and _seed_, Steve Jobs would submit the following JSON, which reflects a correct solution:

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
  "keyFragment": "10100100001001101001011",
  "key": "d0b24f6e5ae62fd2134b",
  "plainText": "university",
  "cipherText": "a5dc26183f945cbb6732"
}
```

### Explanation

The _srn_ and _name_ fields are self-explanatory. The binary _keyFragment_ field has been intercepted (given). The Berlekamp–Massey algorithm can be used to compute the _tap positions_, which is expected to be under the _lfsr_ field in the _taps_ subfield, which is an array of zero-based indices in decreasing order (i.e. [10, 8]). Once knowing the _tap positions_ and the _linear span_ of the LFSR, the entire _key_ can be generated starting from the _seed_, which has been intercepted (given). The _key_ in the result JSON is the key in hexadecimal, i.e. the corresponding value for the following binary number:
 
```
0110100001011001001001111011011100101101

0111001100010111111010010000100110100101
```
 
You should notice 3 things:
- the intercepted _cipherText_ is in hexadecimal and is 10 bytes long, exactly the same length as the generated _key stream_,
- the _key stream_ starts with the given _seed_,
- the _key stream_ contains the the _keyFragment_.
 
Therefore the _plainText_ can be computed from the _cipherText_ and the _key_ with a simple _exclusive or_ (XOR) operation. All strings should be encoded / decoded using UTF-8. There are UTF-8 encoders/decoders available for all programming languages. If you have difficulty decoding, you can double-check yourself with the following Web API call:
 
 http://foley.gold.ac.uk/cw19/api/decode?binary=11101010110111001101001
 
This decodes as __uni__. You can call it with any binary number.

### Final note

You can use the example solution above, which is a well-formed JSON, to adapt for your numbers and your calculation results. As the JSON will be evaluated by an algorithm, every quote, comma, colon, curly brace upper/lower case is crucial. Please pay attention to these. It would be a shame to lose a potential __40%__ of the total marks for this coursework assignment because of a misplaced comma or a missing quote. There are online tools you can use for JSON formatting and validation (for example [this](https://jsonformatter.curiousconcept.com/)), so double-check that your JSON is syntactically correct.
