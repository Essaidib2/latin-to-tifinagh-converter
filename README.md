# latin-to-tifinagh-converter
This Python script is a Latin to Tifinagh alphabet converter with two alternative mappings for greater flexibility in handling character conversions. It allows users to convert text in specific columns of an Excel file from Latin to Tifinagh script.

# Here’s a breakdown of its features and functions:
## Key Features
- Multiple Mappings: The script includes a main mapping (latin_to_tifinagh) from Latin characters to Tifinagh characters, along with two optional alternative mappings (alt_mapping_1 and alt_mapping_2).
- Mapping Detection: The function detect_mapping() can automatically choose a mapping based on specific characters in the text and the user’s choice of conversion option.
- Conversion Function: The latin_to_tifinagh_converter() function processes the text, applying the appropriate mapping and handling two-character sequences like gʷ and kʷ.
- Excel Processing: Users can select a specific column in an Excel file for conversion, and the script will process that column using the specified mapping option. It outputs a new Excel file with the converted text.

# Function Descriptions
- detect_mapping(text, option): Checks for the presence of certain characters to decide which alternative mapping (if any) to apply, based on the user's selected option.
- latin_to_tifinagh_converter(text, option): Converts Latin text to Tifinagh by using the selected mapping (main or alternative) and appends the converted characters to produce the final output.
- column_letter_to_index(letter): Converts a column letter (A, B, C, etc.) to a zero-based index, enabling flexible column selection in Excel processing.
- process_excel_file(file_path, output_path, column_letter, option): Loads an Excel file, converts the specified column, and saves the updated file to a new location. This function uses latin_to_tifinagh_converter to perform the conversion.

# Example Usage
1. Run the script, which will prompt you to select a mapping option.
2. Provide the file paths for the input and output Excel files and the column to convert.
3. The script will process the selected column, applying the Tifinagh conversion, and save the results to the output file.

This script is useful for batch-processing text in Excel files, especially when converting languages with multiple orthographies or alternate character representations.

