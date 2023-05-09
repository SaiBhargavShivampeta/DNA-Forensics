# DNA-Forensics
Thymine (T), Guanine (G), and Cytosine (C), DNA encodes for different proteins which are responsible for the
organism’s functionality. DNA profiling, the process of determining an individual's DNA characteristics, is
commonly used in forensic science, parentage tests, and medical research. However, there are over 3 billion
nitrogenous bases in a typical human genome and comparing every possible alignment to each person being
profiled would be too computationally expensive. So how do we determine which Person a given DNA sequence
belongs to? We leverage the fact that most of the human genome is relatively similar, but there are certain areas
of the human genome that have high genetic diversity. So instead of matching every person’s DNA to the given
DNA, we can compare these highly diverse regions. These regions contain Short Tandem Repeats (STR’s) which
are short sequences of DNA that repeat consecutively.

Using multiple STRs, rather than just one, can improve the accuracy of DNA profiling. If the probability that two
people have the same number of repeats for a single STR is 5%, and the analyst looks at 10 different STRs, then
the probability that two DNA samples match purely by chance is about 1 in 1 quadrillion (assuming all STRs are
independent of each other). So if two DNA samples match in the number of repeats for each of the STRs, the
analyst can be pretty confident they came from the same person.
Suppose we have 3 people (Michael, Reese, and Nathan), with STR counts for ATTA AATG and TATC. Suppose
Michael has 15 consecutive occurrences of ATTA, 10 consecutive occurrences of AATG, and 12 consecutive
occurrences of TATC. Similarly, Reese has 4 consecutive occurrences of ATTA, 6 consecutive occurrences of AATG,
2 consecutive occurrences of TATC and Nathan has 10 consecutive occurrences of ATTA, 4 consecutive
occurrences of AATG, and 2 consecutive occurrences of TATC.

Now suppose you’re given the following DNA Strand:
ATTAATTAATTAATTAAATGAATGAATGAATGAATGAATGTATCTATCATTAAATGTATC

Well, imagine that you looked through the DNA sequence for the longest consecutive sequence of repeated
ATTAs and found that the longest sequence was 4 repeats long. If you then found that the longest sequence of
AATGs is 6 repeats long, and the longest sequence of TATC is 2 repeats long, that would provide pretty good
evidence that the DNA was Reese’s. Notice that the longest consecutive sequence is not simply the overall
count of the STR in the strand.
Of course, it's also possible that once you take the counts for each of the STRs, it doesn't match anyone in your
DNA database, in which case you have no match. If you were given the DNA strand:
ATTAATTAATTAATTAATTA
then there would be no match as none of the persons have only 5 ATTA’s in a row.

 You cannot assume that all DNA databases will contain exactly the same number of STRs (e.g., 3).
To begin the analysis, your first task is to write a program that reads into memory the DNA database. In this
assignment, the DNA database will be encoded as a CSV file, where each row corresponds to an individual and
each column corresponds to an STR. For example,
 Name,ATTA,AATG,TATC
 Michael,15,10,12
 Reese,4,6,2
 Nathan,10,4,2
The DNA database encoded as a CSV file in this manner communicates three important pieces of information.
First, the STRs that we will be using in our analysis (ATTA,AATG,TATC). Second, the names (Michael, Reese, Nathan)
of the individuals involved in our study. Finally, the number of times each individual has a specific STR repeated
consecutively in her/his DNA. Michael has ATTA repeated 15 times consecutively somewhere in his DNA, AATG 10
times, and TATC 12 times. Reese has ATTA repeated 4 times consecutively somewhere in his DNA, AATG 6 times,
and TATC 2 times. Nathan has ATTA repeated 10 times consecutively somewhere in his DNA, AATG 4 times, and
TATC 2 times.

Example
For the CSV file:
Names,AGATG,AATG,TAT
Casey,5,2,8
Amani,3,7,4
Blair,6,1,5
The DNA sequence
AGACGGGTTACCATGACTATTATTATTATTATTATTATTATACGTACGTACGTATGAGATGAGATGAGATGAGAT
would map to Casey,
TATTATTATTATAACCCTGCGCGCGCGCGATCCAGCATTAGCTAGCATCAAGATGAGATGAGATGGAATTTCGAA
to Amani, and
GGTACAGATGGCAAAGATGAGATGAGATGGTCGTCGAGCAATCGTTTCGATAATGAATGAATGAATGAATGAATG
to No match.
