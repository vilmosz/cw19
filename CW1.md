# University of London

# Computing and Information Systems/Creative Computing
# CO3326 Computer security 2018-19

# Coursework assignment 1

__IMPORTANT:__ all students have been allocated a unique set of cipher text, intercepted key stream fragment and seed to use for this coursework assignment. You can obtain this using your Student Reference Number (SRN) from the following URL: http://foley.gold.ac.uk/cw19/api/cw1/{srn}. For example, if your SRN is 877665544, you would obtain your data from [http://foley.gold.ac.uk/cw19/api/cw1/877665544](http://foley.gold.ac.uk/cw19/api/cw1/877665544). If you have difficulties obtaining your cipher text, intercepted key stream fragment and seed, please email us at: [intcomp@gold.ac.uk](intcomp@gold.ac.uk)

This coursework assignment is designed to help you enrich your learning experience and to encourage self-study and creativity. Chapter 5 (pages 49-62) of the subject guide, including the suggested supplementary reading, is a good starting point and will help you in completing this assignment. You should read the coursework assignments carefully and pay particular attention to the [Submission requirements](#submission-requirements).

You are expected to submit __two__ files: a __report__ and a __results sheet__. The _report_ counts as __60%__ of your coursework assignment mark, in which you are expected to answer the questions below. The _results sheet_ counts as __40%__ of your mark, in which you are expected to summarise the results of your calculations in a specific format. Please use the cipher text and keys provided when answering the questions and when compiling the results sheet.

To complete the coursework assignment, it will make your life easier if you write a program. You are welcome to use any programming language. Please include key snippets of your code as an appendix at the end of your report.

\newpage

## Linear Feedback Shift Register

A _linear feedback shift register_ (LFSR) is a type of counter that generates a "pseudo random" sequence of bits, which is particularly useful in cryptography. In simple terms, it is a register of bits that performs discrete step operations that:

- shifts all of the bits one position to the left, and
- replaces the vacated bit by the _exclusive or_ (XOR) of certain bits shifted off, indicated by the _tap_ positions.

A LFSR has three parameters that characterise the sequence of bits it produces: the number of bits _N_, the initial _seed_ (the sequence of bits that initialises the register), and the the tap positions _tap_. The following picture illustrates one step of an 11-bit LFSR with initial seed 11010000101 and tap positions 10 and 8.

![One step of an 11-bit LFSR with initial seed 11010000101 and tap positions at bits 10 and 8](https://raw.githubusercontent.com/vilmosz/cw19/master/LFSR.png)

Please do some research around LFSRs, starting from your subject guide (Chapter 5), suggested readings and [Wikipedia](https://en.wikipedia.org/wiki/Linear-feedback_shift_register). Make sure you also understand the [Berlekamp-Massey algorithm](https://en.wikipedia.org/wiki/Berlekamp%E2%80%93Massey_algorithm) as this is necessary for you to complete the coursework assignment.

\newpage

## Assignment

Suppose you are an avid hacker working for a security agency and you intercept a _cipher text_, a _key stream fragment_ and a _seed_ that you know has been sent using a cryptosystem based on LFSRs. You would like to decrypt the message.

__IMPORTANT:__ To answer the questions below, please use the _cipher text_, intercepted _key stream fragment_ and _seed_ that you obtained using your SRN.

#### Question 1
Briefly describe how stream ciphers work and give a few reasons why stream ciphers based on linear-feedback shift registers are so popular.

#### Question 2
Explain the following terms in the context of LFSRs: _feedback function_, _primitive polynomial_ and _cycle_. What are _maximal-length polynomials_?

#### Question 3
Explain why the use of LFSRs on their own is insufficient to provide good security. List three schemes that have been proposed to increase the security of LFSRs.

#### Question 4
Briefly describe, in your own words, what the Berlekamp-Massey algorithm is used for and how it works.

#### Question 5
Apply the Berlekamp-Massey algorithm on the key stream fragment you were given to obtain the _feedback polynomial_ that generated the key. For full marks, you have to implement the algorithm yourself, attach key parts of the algorithm to the report as an appendix and describe briefly which bit of the implementation you found the most challenging. If you use someone else's code or an online service you will not be awarded full marks; in this case make sure you acknowledge the source of the code or service you use.

#### Question 6
Generate the full key stream in order to be able to decrypt the cipher text you intercepted (_i.e._ what you were given).

#### Question 7
Decrypt and decode the cipher text to get the original plain text message. Show all your workings. If your calculations are correct, you will get an English dictionary word as the plain text.

#### Question 8
Briefly - in one paragraph - describe the design of your code. Attach key snippets to the annex. Do not forget to acknowledge all sources. Make sure you acknowledge any code re-use.


## Submission requirements

__REMINDER:__ It is important that your submitted coursework assignment is your own individual work and, for the most part, written in your own words. You must provide appropriate in-text citation for both paraphrase and quotation, with a detailed reference section at the end of your coursework. Copying, plagiarism and unaccredited and wholesale reproduction of material from books or from any online source is unacceptable, and will be penalised (see our [guide on how to avoid plagiarism on the VLE](https://computing.elearning.london.ac.uk/mod/page/view.php?id=5176)).

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

\newpage

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

The _srn_ and _name_ fields are self-explanatory. The binary _keyFragment_ field has been intercepted (given). The Berlekamp–Massey algorithm can be used to compute the _tap positions_, which is expected to be under the _lfsr_ field in the _taps_ subfield, which is an array of zero-based indices in decreasing order (_i.e._ [10, 8]). Once the _tap positions_ and the _linear span_ of the LFSR are known, the entire _key_ can be generated starting from the _seed_, which has been intercepted (given). The _key_ is the full-length key stream in hexadecimal that is necessary to decrypt the _cipherText_. The corresponding binary value for the _key_ in this case is:

```
1101000010110010010011110110111001011010
1110011000101111110100100001001101001011
```

The _cipherText_ is also given in hexadecimal, so this needs to be converted to binary before the _key_ can be applied on it, _i.e._ a simple _exclusive or_ (XOR) operation, to get the encoded plain text. The binary encoded plain text can then be decoded to obtain the actual _plainText_, which is a recognisable English dictionary word.

You should notice the following:

- The intercepted _cipherText_ is in hexadecimal and is 10 bytes long, exactly the same length as the generated _key stream_.
- The _key stream_ starts with the given _seed_.
- The _key stream_ contains the the _keyFragment_.

All strings are encoded/decoded using UTF-8. There are UTF-8 encoders/decoders available for all programming languages. If you have difficulties decoding, you can double-check your results with the following Web API call: [http://foley.gold.ac.uk/cw19/api/decode?binary=11101010110111001101001](http://foley.gold.ac.uk/cw19/api/decode?binary=11101010110111001101001). This decodes as __uni__. You can call this with any binary number.

### Final note

You can use the example solution above as a template, which is a well-formed JSON, and replace the values with your data and calculation results. As the JSON will be evaluated by an algorithm, every quote, comma, colon, curly brace upper/lower case is crucial. Please pay attention to these. It would be a shame to lose a potential __40%__ of the total marks for this coursework assignment because of a misplaced comma or a missing quote. There are online tools you can use for JSON formatting and validation (for example [https://jsonformatter.curiousconcept.com](https://jsonformatter.curiousconcept.com)), so double-check that your JSON is syntactically correct.
