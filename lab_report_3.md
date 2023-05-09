# Lab Report 3

## **Objectives:**

1. Choose a command to explore.

2. Give two examples for each command-line option.

3. Cite the sources.


## **1: Choose a command to explore**

### `grep` Command:

I chose the command `grep` to explore. `grep` is used to perform a "filter-search" on a file to find particular words or characters in it. 
Its four command-line options that I will be exploring are as following:

*[Note: I have added smaller descriptions in parentheses of each command-line option which makes them easy to remember.]*

1. `-i`: (ignores case) this command-line options allows you to find **case-insensitive** matches of the pattern of given word or character.
2. `-n`: (numbers and lines) this command-line option outputs the lines and their numbers that match the pattern of given word or character.
3. `-c`: (count of lines) this command-line option outputs the number of lines that match the pattern of given word or character.
4. `-w`: (whole word) this command-line option allows you find the lines that match the given word or character precisely.

## **2: Give two examples for each command-line option**

*[Note: To show the examples, I used the 'pmed.0020157.txt' from plos file in the stringsearch-data provided to us.]*

The text file that I will be performing these commands on is as below:

```
Turner and Tramèr provide a cogent argument in favor of the ethical use of placebo
controls despite “proven effective treatment” [1]. However, they are wide of the mark
citing the APPROVe trial in support of their position. Because there is no established
treatment to prevent adenomatous polyps, few commentators would have any objections to the
use of placebo controls in this study. Nevertheless, they are right to suggest that it
would have been desirable to have included a placebo control in the VIGOR study to provide
a more rigorous assessment of safety. Whether, all things considered, a placebo control
would have been ethical in this study of treatment for rheumatoid arthritis is
debatable.
Another issue not discussed in this 
PLoS Medicine Debate is the value of placebo controls in early “proof of
concept” efficacy trials, despite the existence of established treatment. The efficiency of
seeking a rigorous efficacy signal before moving on to larger-scale trials (and exposing as
few subjects as possible to drugs that might not work or turn out to be toxic) is a valid
ethical reason for using placebo controls, provided subjects are not exposed to undue risks
of harm from withholding established treatment [2].
```

***

**Two examples for command-line option, `-i`:**

> Example #1

```
[sarveshmann]:plos:189$ grep -i "appro" pmed.0020157.txt
        citing the APPROVe trial in support of their position. Because there is no established
```

**Explanation:** Here the command `grep -i` searches for the pattern that matches the given pattern *"appro"* in the text file and prints out the lines that contains it. Notice, the case of the letters do not matter here, as the command found it even tho, in the text, the pattern is in uppercase letters.  

> Example #2

```
[sarveshmann]:plos:190$ grep -i "pl" pmed.0020157.txt
        Turner and Tramèr provide a cogent argument in favor of the ethical use of placebo
        use of placebo controls in this study. Nevertheless, they are right to suggest that it
        would have been desirable to have included a placebo control in the VIGOR study to provide
        a more rigorous assessment of safety. Whether, all things considered, a placebo control
        PLoS Medicine Debate is the value of placebo controls in early “proof of
        ethical reason for using placebo controls, provided subjects are not exposed to undue risks
```

**Explanation:** Here the command `grep -i` searches for the pattern that matches the given pattern *"pl"* in the text file and prints out the lines that contains it. Notice, the rest of the pattern doesn't matter here as any word that contains "pl" in it will also be printed.

***

**Two examples for command-line option, `-n`:**

> Example #1

```
[sarveshmann]:plos:191$ grep -n "Turner" pmed.0020157.txt                           
6:        Turner and Tramèr provide a cogent argument in favor of the ethical use of placebo
```

**Explanation:** Here the command `grep -n` searches for the lines that that contain the given pattern "Turner" and prints them out along with their number. In this case, the line number is 6 (printed on the very left).

> Example #2

```
[sarveshmann]:plos:193$ grep -n "PLoS" pmed.0020157.txt
16:        PLoS Medicine Debate is the value of placebo controls in early “proof of
```

**Explanation:** Here the command `grep -n` searches for the lines that that contain the given pattern "PLoS" and prints them out along with their number. In this case, the line number is 16 (printed on the very left).

***

**Two examples for command-line option, `-c`:**

> Example #1

```
[sarveshmann]:plos:194$ grep -c "treatment" pmed.0020157.txt
5
```

**Explanation:** Here the command `grep -c` searches for the lines that that contain the given pattern "treatment" and prints out the count of all line that contains it. In this case, the count is 5 (printed on the very left).

> Example #2

```
[sarveshmann]:plos:196$ grep -c "VIGOR" pmed.0020157.txt
1
```

**Explanation:** Here the command `grep -c` searches for the lines that that contain the given pattern "VIGOR" and prints out the count of all line that contains it. In this case, the count is 1 (printed on the very left).

***

**Two examples for command-line option, `-w`:**

> Example #1

```
[sarveshmann]:plos:198$ grep -w "as" pmed.0020157.txt  
        seeking a rigorous efficacy signal before moving on to larger-scale trials (and exposing as
        few subjects as possible to drugs that might not work or turn out to be toxic) is a valid
```

**Explanation:** Here the command `grep -w` searches for the lines that that contain the given pattern "as" precisely and prints out the lines that contains it. Notice, only those lines are printed that contains the word "as" exactly, and not the other ones that maybe have "as" in the spelling of a word.

> Example #2

```
[sarveshmann]:plos:199$ grep -w "to" pmed.0020157.txt
        treatment to prevent adenomatous polyps, few commentators would have any objections to the
        use of placebo controls in this study. Nevertheless, they are right to suggest that it
        would have been desirable to have included a placebo control in the VIGOR study to provide
        seeking a rigorous efficacy signal before moving on to larger-scale trials (and exposing as
        few subjects as possible to drugs that might not work or turn out to be toxic) is a valid
        ethical reason for using placebo controls, provided subjects are not exposed to undue risks
```

**Explanation:** Here the command `grep -w` searches for the lines that that contain the given pattern "to" precisely and prints out the lines that contains it. Notice, only those lines are printed that contains the word "as" exactly, and not the other ones that maybe have "to" in the spelling of a word.

***

## **3: Cite the sources**

* [GeeksforGeeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)
* [stringsearch-data](https://github.com/ucsd-cse15l-s23/stringsearch-data)


# *Thank you for your time!*
