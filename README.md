# File-compressor-and-decompressor
This project is based on Huffman Coding, a lossless, bottom-up compression algorithm. It can compress and decompress any text files.

# Huffman coding:
In computer science and information theory, a Huffman code is a particular type of optimal prefix code that is commonly used for lossless data compression. The process of finding or using such a code proceeds by means of Huffman coding, an algorithm developed by David A. Huffman while he was a Sc.D. student at MIT, and published in the 1952 paper "A Method for the Construction of Minimum-Redundancy Codes".

The output from Huffman's algorithm can be viewed as a variable-length code table for encoding a source symbol (such as a character in a file). The algorithm derives this table from the estimated probability or frequency of occurrence (weight) for each possible value of the source symbol. As in other entropy encoding methods, more common symbols are generally represented using fewer bits than less common symbols. Huffman's method can be efficiently implemented, finding a code in time linear to the number of input weights if these weights are sorted. However, although optimal among methods encoding symbols separately, Huffman coding is not always optimal among all compression methods - it is replaced with arithmetic coding or asymmetric numeral systems if better compression ratio is required.

# Implementation in Project
This project supports two functions:
1) Encode: Compresses input file passed.
2) Decode: Decompresses Huffman encoded file back to its original file with no data loss compared to the original input file(the original data will always be perfectly restructured from the compressed data) .

Huffman class contains two public functions
1) compress()
2) decompress()
And a constructor which accepts input file and output file.

***Compressing file:***

compress(): Following are the steps followed to compress the input file. <br> <br>
1)createMinHeap(): This function reads the input file and stores the frequency of all the characters appearing in the file. It further creates a Min Heap structure based on the frequency of each character using priority queue as a data structure that stores Nodes and uses its frequency as a comparing parameter. <br> <br>
2)createTree(): This function generates the Huffman tree by duplicating the Min Heap created earlier keeping the original Min Heap. It pops the two Nodes with the lowest frequency. Further, it assigns these two as left and right nodes to a new Node with a frequency which is the sum of the two popped nodes and pushes this Node back to the Min Heap. This process is continued until Min Heap has a size equal to 1. <br> <br>
3)createCodes(): This function traverses the entire Huffman tree and assigns codes in binary format to every Node. <br> <br>
4)saveEncodedFile(): This function saves the Huffman encoded input file to the output file. The image below illustrates how the output file is written. <br/> <br/>
![compressing1](https://user-images.githubusercontent.com/97902984/192035098-4d3ab039-09b2-4a8d-a43f-28cdb5801814.png) <br>
minHeap = ({character data} {huffman code for that character}) * minheapsize <br>
{huffman code for that character} = 128 bits divided into 16 decimal numbers. Every number represents 8 bit binary number.
eg: {127 - code.length()} * '0' + '1' (representing start bit) + code = 128 bits
It is converted to 16 * 8-bit decimal numbers = 128 bits
{Encoded input File characters} {count0} = Entire file is converted into its huffman encoded form which is a binary code. This binary string is divided in 8-bit decimal numbers. If the final remaining bits are less than 8 bits, (8 - remainingBits) number of '0's are appended at the end. count0 is the number of '0's appended at the end.
The output file should be (.huf) file which represents it is a Huffman encoded file.

***Decompressing file:*** <br>
decompress(): Following are the steps followed to decompress the Huffman encoded file.

1)getTree(): This function reads the Min Heap stored at the beginning of the file and reconstructs the Huffman tree by appending one Node at a time. MinHeapSize is the first value, next {MinHeapSize * (1+16)} contains character data and 16 decimal values representing 128 bits of binary Huffman code. Ignore the initial (127 - code.length()) of '0's and starting '1' bit and append the Node.

2)saveDecodedFile(): This function reads the entire {Encoded input File charachters} and {count0} by ignoring the first {MinHeapSize * (1 + 16)} of the file. The decimal values are converted to their binary equivalent(huffman codes) and the resulting character is appended to the output file by traversing the reconstructed huffman tree. The final count0 number of '0's are ignored since they were extra bits added while saving the encoded file.

# How To Run:
***For compression use the following command*** <br>
![Screenshot (376)](https://user-images.githubusercontent.com/97902984/192038107-e74e7f5c-6177-4b2e-81be-93897fc2422e.png)

***For decompression use the following command***<br>
![Screenshot (380)](https://user-images.githubusercontent.com/97902984/192038251-adf68eb8-2ded-48df-a79a-c94b4250ef3a.png)
