# House Number Rangifier

## Description
This Python script converts sequences of house numbers into ranges, removes duplicates, and sorts values. It's adaptable to different formats, including the Ukrainian convention of using 'Буд' (short for 'Будинок', meaning 'Building' in Ukrainian) at the beginning of strings. Users can replace 'Буд' with their own term if needed or leave it unused.

## Usage
1. Run the script.
2. Enter the input string. You can use 'Enter' for a test string, 'q' to exit, or 'i' for info.
3. Optionally, choose to delete slashes and numbers after them by entering '/'.
4. The script will display the formatted output string.

## Example
Input string: 1,2,2B,3,5,4,6,9,10-12-15,22,55,77,78,1,3,21,24,23,26,27.28,5/74

Output string: 1-6,9-15,21-24,26-28,55,77-78,2B,5/74

