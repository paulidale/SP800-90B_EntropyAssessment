# SP800-90B_EntropyAssessment (DRAFT)
Cryptographic random bit generators (RBGs), also known as random number generators (RNGs), require a noise source that produces digital outputs with some level of unpredictability, expressed as min-entropy. 
The SP800-90B_EntropyAssessment python package implements the min-entropy assessment methods included in the 2016 draft of Special Publication 800-90B.

Please note that this code package was published to assist in the evaluation of the entropy estimation methods provided in the draft publication. As such, it is written to resemble the pseudocode in the draft, and is not optimized for performance. After SP 800-90B is finalized, the code will be ported to another language and performance improvements will be made.

## Disclaimer
NIST-developed software is provided by NIST as a public service. You may use, copy and distribute copies of the software in any medium, provided that you keep intact this entire notice. You may improve, modify and create derivative works of the software or any portion of the software, and you may copy and distribute such modifications or works. Modified works should carry a notice stating that you changed the software and should note the date and nature of any such change. Please explicitly acknowledge the National Institute of Standards and Technology as the source of the software.

NIST-developed software is expressly provided ?AS IS.? NIST MAKES NO WARRANTY OF ANY KIND, EXPRESS, IMPLIED, IN FACT OR ARISING BY OPERATION OF LAW, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTY OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, NON-INFRINGEMENT AND DATA ACCURACY. NIST NEITHER REPRESENTS NOR WARRANTS THAT THE OPERATION OF THE SOFTWARE WILL BE UNINTERRUPTED OR ERROR-FREE, OR THAT ANY DEFECTS WILL BE CORRECTED. NIST DOES NOT WARRANT OR MAKE ANY REPRESENTATIONS REGARDING THE USE OF THE SOFTWARE OR THE RESULTS THEREOF, INCLUDING BUT NOT LIMITED TO THE CORRECTNESS, ACCURACY, RELIABILITY, OR USEFULNESS OF THE SOFTWARE.

You are solely responsible for determining the appropriateness of using and distributing the software and you assume all risks associated with its use, including but not limited to the risks and costs of program errors, compliance with applicable laws, damage to or loss of data, programs or equipment, and the unavailability or interruption of operation. This software is not intended to be used in any situation where a failure could cause risk of injury or damage to property. The software developed by NIST employees is not subject to copyright protection within the United States.

The identification of any commercial product or trade name does not imply endorsement or recommendation by the National Institute of Standards and Technology, nor is it intended to imply that the materials or equipment identified are necessarily the best available for the purpose.

## Requirements

This code package requires 64-bit Python 2.7 or Python 3.

## Summary of Changes
1. updated for second draft of SP 800-90B (January 2016)

## Basic Usage

There are three main files in this code package: iid_main.py, noniid_main.py, and restart.py. Brief usage descriptions are listed below. For further details, please refer to the user guide.

## Using iid_main.py
The file iid_main.py calls all of the tests that determine whether or not the input file appears to contain independent and identically distributed (IID) samples, and if so, gives an entropy assessment. 
The program takes three arguments: 

1. 	datafile: a binary file containing the samples to be tested.
2. 	bits_per_symbol: the number of bits required to represent the largest output symbol from the noise source. E.g., if the largest value is 12, this would be 4.

### Example
	> python iid_main.py truerand_1bit.bin 1
	reading 1000000 bytes of data
	IID = True
	min-entropy = 0.995043
	
	Don't forget to run the sanity check on a restart dataset using H_I = 0.995043

## Using noniid_main.py
The file noniid_main.py calls all of the min-entropy estimation methods. The program requires two arguments:

1. 	datafile: a binary file containing the samples to be tested.
2. 	bits_per_symbol: the number of bits required to represent the largest output symbol from the noise source. E.g., if the largest value is 12, this would be 4.

### Example
Non-IID estimators applied to same data as above:

	> python noniid_main.py truerand_4bit.bin 4
	reading 1000000 bytes of data
	min-entropy = 3.70057

	Don't forget to run the sanity check on a restart dataset using H_I = 3.70057

## Using restart.py
The file restart.py performs the sanity checks on the restart dataset. The program requires three arguments:

1. 	datafile: a binary file containing the samples to be tested.
2. 	bits_per_symbol: the number of bits required to represent the largest output symbol from the noise source. E.g., if the largest value is 12, this would be 4.
3.	H_I: initial entropy estimate obtained via iid_main.py or noniid_main.py.

### Example
	> python restart.py truerand_4bit.bin 4 3.70057
	reading 1000000 bytes of data
	Passed the restart tests
	*** Final entropy estimate: 3.700570

## More Information
For more information on using this code, such as optional arguments, see the user guide in this repository.
For more information on the estimation methods, see [SP 800-90B second draft](http://csrc.nist.gov/publications/drafts/800-90/sp800-90b_second_draft.pdf).

### Contact Information
This code is currently maintained by Kerry McKay and John Kelsey.
