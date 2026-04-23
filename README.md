# csv-data-cleaner
import csv

input_file = "raw_data.csv"
output_file = "cleaned_data.csv"

with open(input_file, mode='r', newline='') as infile:
    reader = csv.DictReader(infile)
    
    cleaned_rows = []

    for row in reader:
        # Clean name (capitalize)
        row['name'] = row['name'].strip().title()
        
        # Clean email (lowercase)
        row['email'] = row['email'].strip().lower()
        
        # Skip rows with missing data
        if row['name'] and row['email']:
            cleaned_rows.append(row)

with open(output_file, mode='w', newline='') as outfile:
    fieldnames = ['name', 'email']
    writer = csv.DictWriter(outfile, fieldnames=fieldnames)
    
    writer.writeheader()
    writer.writerows(cleaned_rows)

print("Data cleaned successfully!")
