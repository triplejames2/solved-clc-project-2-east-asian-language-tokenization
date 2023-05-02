Download Link: https://assignmentchef.com/product/solved-clc-project-2-east-asian-language-tokenization
<br>



For this project you have a choice between implementing Thai tokenization or Japanese tokenization.

<h1>Thai Tokenization</h1>

You will take a finite state approach to Thai tokenization.  This is a simplified FSA that will work on the examples provided, but may not work on every Thai sentence.

./thai_tokenizer.py &lt;input_file&gt; &lt;output_file&gt;

Characters in Thai can be categorized as follows:

<table width="0">

 <tbody>

  <tr>

   <td colspan="2" width="207"><strong>Category</strong></td>

   <td width="241"><strong>Members</strong></td>

   <td width="246"><strong>Unicode</strong></td>

  </tr>

  <tr>

   <td width="47"><strong>V1</strong></td>

   <td width="159">Preposed vowel</td>

   <td width="241">เแโใไ</td>

   <td width="246">0E40, 0E41, 0E42, 0E43, 0E44</td>

  </tr>

  <tr>

   <td width="47"><strong>C1</strong></td>

   <td width="159">Initialconsonant</td>

   <td width="241">กขฃคฅฆงจ ฉชซฌญฎฏฐฑฒณดตถ ทธนบปผฝพ ฟภมยรฤลฦ วศษสหฬอฮ</td>

   <td width="246">0E01 – 0E2E</td>

  </tr>

  <tr>

   <td width="47"><strong>C2</strong></td>

   <td width="159">Clustered consonant</td>

   <td width="241">รลวนม</td>

   <td width="246">0E19, 0E21, 0E23, 0E25, 0E27</td>

  </tr>

  <tr>

   <td width="47"><strong>V2</strong></td>

   <td width="159">Super/subscript vowel</td>

   <td width="241">◌ิ ◌ี ◌ึ ◌ื ◌ุ ◌ู ◌ั ◌็</td>

   <td width="246">0E31, 0E34, 0E35, 0E36, 0E37, 0E38, 0E39, 0E47</td>

  </tr>

  <tr>

   <td width="47"><strong>T</strong></td>

   <td width="159">Superscript tonemark</td>

   <td width="241">◌่◌้◌๊◌๋</td>

   <td width="246">0E48, 0E49, 0E4A, 0E4B</td>

  </tr>

  <tr>

   <td width="47"><strong>V3</strong></td>

   <td width="159">Postposed vowel</td>

   <td width="241">าอยว</td>

   <td width="246">0E22, 0E27, 0E2D, 0E32</td>

  </tr>

  <tr>

   <td width="47"><strong>C3</strong></td>

   <td width="159">Final consonant</td>

   <td width="241">งนมดบกยว</td>

   <td width="246">0E01, 0E07, 0E14, 0E19, 0E1A, 0E21, 0E22, 0E27</td>

  </tr>

 </tbody>

</table>

Every word has a consonant from the list of initial consonants, but characters from the other categories may or may not appear in a word.  They appear in the following order:

V1? C1 C2? V2? T? V3? C3?

The states and transitions are as follows:

<table width="0">

 <tbody>

  <tr>

   <td colspan="2" width="164"><strong>v1</strong></td>

   <td width="58"><strong>c1</strong></td>

   <td width="89"><strong>c2</strong></td>

   <td width="78"><strong>v2</strong></td>

   <td width="73"><strong>t</strong></td>

   <td width="74"><strong>v3</strong></td>

   <td width="57"><strong>c3</strong></td>

   <td width="78"><strong>#</strong></td>

  </tr>

  <tr>

   <td width="72"><strong>q0</strong></td>

   <td width="93">q1</td>

   <td width="58">q2</td>

   <td width="89">–</td>

   <td width="78">–</td>

   <td width="73">–</td>

   <td width="74">–</td>

   <td width="57">–</td>

   <td width="78">–</td>

  </tr>

  <tr>

   <td width="72"><strong>q1</strong></td>

   <td width="93">–</td>

   <td width="58">q2</td>

   <td width="89">–</td>

   <td width="78">–</td>

   <td width="73">–</td>

   <td width="74">–</td>

   <td width="57">–</td>

   <td width="78">–</td>

  </tr>

  <tr>

   <td width="72"><strong>q2</strong></td>

   <td width="93">q7</td>

   <td width="58">q8</td>

   <td width="89">q3</td>

   <td width="78">q4</td>

   <td width="73">q5</td>

   <td width="74">q6</td>

   <td width="57">q9</td>

   <td width="78">–</td>

  </tr>

  <tr>

   <td width="72"><strong>q3</strong></td>

   <td width="93">–</td>

   <td width="58">–</td>

   <td width="89">–</td>

   <td width="78">q4</td>

   <td width="73">q5</td>

   <td width="74">q6</td>

   <td width="57">q9</td>

   <td width="78">–</td>

  </tr>

  <tr>

   <td width="72"><strong>q4</strong></td>

   <td width="93">q7</td>

   <td width="58">q8</td>

   <td width="89">–</td>

   <td width="78">–</td>

   <td width="73">q5</td>

   <td width="74">q6</td>

   <td width="57">q9</td>

   <td width="78">–</td>

  </tr>

  <tr>

   <td width="72"><strong>q5</strong></td>

   <td width="93">q7</td>

   <td width="58">q8</td>

   <td width="89">–</td>

   <td width="78">–</td>

   <td width="73">–</td>

   <td width="74">q6</td>

   <td width="57">q9</td>

   <td width="78">–</td>

  </tr>

  <tr>

   <td width="72"><strong>q6</strong></td>

   <td width="93">q7</td>

   <td width="58">q8</td>

   <td width="89">–</td>

   <td width="78">–</td>

   <td width="73">–</td>

   <td width="74">–</td>

   <td width="57">q9</td>

   <td width="78">–</td>

  </tr>

  <tr>

   <td width="72"><strong>q7</strong></td>

   <td width="93">–</td>

   <td width="58">–</td>

   <td width="89">–</td>

   <td width="78">–</td>

   <td width="73">–</td>

   <td width="74">–</td>

   <td width="57">–</td>

   <td width="78">q1</td>

  </tr>

  <tr>

   <td width="72"><strong>q8</strong></td>

   <td width="93">–</td>

   <td width="58">–</td>

   <td width="89">–</td>

   <td width="78">–</td>

   <td width="73">–</td>

   <td width="74">–</td>

   <td width="57">–</td>

   <td width="78">q2</td>

  </tr>

  <tr>

   <td width="72"><strong>q9</strong></td>

   <td width="93">–</td>

   <td width="58">–</td>

   <td width="89">–</td>

   <td width="78">–</td>

   <td width="73">–</td>

   <td width="74">–</td>

   <td width="57">–</td>

   <td width="78">q0</td>

  </tr>

 </tbody>

</table>

If the state becomes 7 or 8, the FSA has encountered a new starting vowel or consonant, insert a space <strong>before</strong> the character that initiated the transition.  From state 7 or 8, transition to state 1 or 2 (respectively), before looking at the next character.

If the state becomes 9, the FSA has encountered a final consonant, insert a space <strong>after</strong> the character that initiated the transition.  From state 9, transition to state 0. Note that there are overlaps in the categories!  (The characters in C2, C3, and V3 overlap with C1).  To deal with this, accept the characters in the following order:

<table width="0">

 <tbody>

  <tr>

   <td colspan="2" width="612"><strong>Character Class Order</strong></td>

  </tr>

  <tr>

   <td width="93"><strong>q0</strong></td>

   <td width="519">V1, C1</td>

  </tr>

  <tr>

   <td width="93"><strong>q1</strong></td>

   <td width="519">C1</td>

  </tr>

  <tr>

   <td width="93"><strong>q2</strong></td>

   <td width="519">C2, V2, T, V3, C3, V1, C1</td>

  </tr>

  <tr>

   <td width="93"><strong>q3</strong></td>

   <td width="519">V2, T, V3, C3</td>

  </tr>

  <tr>

   <td width="93"><strong>q4</strong></td>

   <td width="519">T, V3, C3, V1, C1</td>

  </tr>

  <tr>

   <td width="93"><strong>q5</strong></td>

   <td width="519">V3, C3, V1, C1</td>

  </tr>

  <tr>

   <td width="93"><strong>q6</strong></td>

   <td width="519">C3, V1, C1</td>

  </tr>

  <tr>

   <td width="93"><strong>q7</strong></td>

   <td width="519"> </td>

  </tr>

  <tr>

   <td width="93"><strong>q8</strong></td>

   <td rowspan="2" width="519"> </td>

  </tr>

  <tr>

   <td width="93"><strong>q9</strong></td>

  </tr>

 </tbody>

</table>

The sample_out.txt file contains the correctly tokenized output of the in.txt file.  Please check your program output against this file.

<h1>Japanese Tokenization</h1>

For the Japanese tokenization project, you will use the MaxMatch algorithm to read in a file with lines of Japanese text without spaces, find the word boundaries, and output a file with the same lines of text with spaces added between words.

./japanese_tokenizer.py &lt;input_file&gt; &lt;output_file&gt;

The MaxMatch algorithm uses a dictionary (japanese_wordlist.txt).  Starting from the beginning of the sentence, match the longest consecutive string of characters that exists in the dictionary.  Once you have found that longest string, insert a space and continue.  If no matches exist in the dictionary, consider the character a one character word, insert a space and continue.

The sample_out.txt file contains the correctly tokenized output of the in.txt file.  Please check your program output against this file.

gold_standard.txt contains the ideal tokenization.  The MaxMatch algorithm makes mistakes, so don’t expect your tokenization output to match this.  When you’re done implementing MaxMatch, compare the output of your file to the gold_standard.  Make a file (by hand or programmatically) named evaluation.txt that contains the following:

# of sentences tokenized correctly:  &lt;# of lines of output that match gold_standard&gt;

# of sentences tokenized incorrectly: &lt;# of lines of output that don’t match gold_standard&gt;

accuracy: &lt;# correct / total # of sentences&gt;