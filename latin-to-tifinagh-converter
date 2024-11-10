import pandas as pd
import string

# Latin to Tifinagh Alphabet Converter with Multiple Alternative Mappings

# Main Latin to Tifinagh mapping
latin_to_tifinagh = {
    'a': 'ⴰ', 'b': 'ⴱ', 'g': 'ⴳ', 'gʷ': 'ⴳⵯ', 'd': 'ⴷ', 'ḍ': 'ⴹ',
    'e': 'ⴻ', 'f': 'ⴼ', 'k': 'ⴽ', 'kʷ': 'ⴽⵯ', 'h': 'ⵀ', 'ḥ': 'ⵃ',
    'ɛ': 'ⵄ', 'x': 'ⵅ', 'q': 'ⵇ', 'i': 'ⵉ', 'j': 'ⵊ', 'l': 'ⵍ',
    'm': 'ⵎ', 'n': 'ⵏ', 'u': 'ⵓ', 'r': 'ⵔ', 'ṛ': 'ⵕ', 'ɣ': 'ⵖ',
    's': 'ⵙ', 'ṣ': 'ⵚ', 'c': 'ⵛ', 't': 'ⵜ', 'ṭ': 'ⵟ', 'w': 'ⵡ',
    'y': 'ⵢ', 'z': 'ⵣ', 'ẓ': 'ⵥ'
}

# Alternative mapping 1 (Option 1)
alt_mapping_1 = {
    'å': 'ⴳⵯ', 'ä': 'ⴹ', 'æ': 'ⴽⵯ', 'p': 'ⵃ', 'o': 'ⵄ', 'v': 'ⵖ',
    'ë': 'ⵕ', 'ã': 'ⵚ', 'ï': 'ⵟ', 'ç': 'ⵥ'
}

# Alternative mapping 2 (Option 2)
alt_mapping_2 = {
    'S': 'ⵚ', 'T': 'ⵟ', 'Z': 'ⵥ', 'H': 'ⵃ', 'D': 'ⴹ', 'R': 'ⵕ', 'v': 'ⵖ'
}

def detect_mapping(text, option):
    """Automatically detect the appropriate mapping based on specific characters and the chosen option."""
    if option == 1:
        if any(char in alt_mapping_1 for char in text):
            return alt_mapping_1
        else:
            return None  # Default to the original mapping
    elif option == 2:
        return alt_mapping_2

def latin_to_tifinagh_converter(text, option):
    """Convert Latin text to Tifinagh using the selected mapping."""
    result = []
    i = 0
    while i < len(text):
        if i < len(text) - 1 and text[i:i+2].lower() in ['gʷ', 'kʷ']:
            char = text[i:i+2].lower()
            i += 2
        else:
            char = text[i]
            i += 1
        
        # Detect mapping based on the selected option
        alt_mapping = detect_mapping(text, option)
        
        if alt_mapping and char in alt_mapping:
            result.append(alt_mapping[char])
        elif char.lower() in latin_to_tifinagh:
            result.append(latin_to_tifinagh[char.lower()])
        else:
            result.append(char)
    
    return ''.join(result)

def column_letter_to_index(letter):
    """Convert column letter (A, B, C, ...) to zero-based index."""
    return string.ascii_uppercase.index(letter.upper())

def process_excel_file(file_path, output_path, column_letter, option):
    # Load the Excel file
    df = pd.read_excel(file_path)
    
    # Convert column letter to zero-based index
    try:
        column_index = column_letter_to_index(column_letter)
    except ValueError:
        print(f"Invalid column letter '{column_letter}'.")
        return
    
    # Ensure the index is within the range of available columns
    if column_index >= len(df.columns):
        print(f"Column '{column_letter}' is out of range for the available columns.")
        return
    
    # Get the actual column name from the DataFrame using the index
    column_name = df.columns[column_index]
    
    # Apply conversion to the specified column
    df[column_name] = df[column_name].apply(lambda cell_value: latin_to_tifinagh_converter(str(cell_value), option))
    
    # Save the modified file to a new Excel file
    df.to_excel(output_path, index=False)
    print(f"Converted file saved to: {output_path}")

# Example usage
print("Latin to Tifinagh Converter")
print("---------------------------")
print("Choose conversion mode:")
print("1 - Original mapping with automatic switch to Alternative Mapping 1")
print("2 - Use Alternative Mapping 2")

while True:
    option = input("Enter option (1 or 2): ")
    if option in ['1', '2']:
        option = int(option)
        break
    print("Invalid input. Please enter 1 or 2.")

# File paths and column letter
input_file = input("Enter the path of the input Excel file: ")
output_file = input("Enter the path for the output Excel file: ")
column_letter = input("Enter the column letter to convert (A, B, C, ...): ")

# Process the Excel file with the selected option
process_excel_file(input_file, output_file, column_letter, option)
