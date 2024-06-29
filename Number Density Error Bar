import numpy as np                 #importing module for numerical operations
import matplotlib.pyplot as plt    #ensuring plotting is possible
import ezodf                       #importing module for reading ODS files

# Path to the averaged number density 

ods_file_path = '/content/average.ods' 

# Function to read averaged data from ODS file

def read_averaged_data(file_path):
    try:
        doc = ezodf.opendoc(file_path)
        sheet = doc.sheets[0]

        # Reading the values
        averaged_values = []
        for row in sheet.rows():
            for cell in row:
                if cell.value is not None:
                    averaged_values.append(float(cell.value))

        return averaged_values

    except Exception as e:
        print(f"Error reading data from {file_path}: {e}")
        return None

averaged_values = read_averaged_data(ods_file_path)

# If data was successfully read, proceeding with calculations and plotting
if averaged_values is not None:
    # Calculating standard deviation (SD) and standard error
    sd = np.std(averaged_values)
    se = sd / np.sqrt(len(averaged_values))

    # Choose every n-th data point to plot
    n = 10  # Change this value to control the number of error bars
    sampled_indices = np.arange(0, len(averaged_values), n)
    sampled_values = [averaged_values[i] for i in sampled_indices]

    # Plotting
    plt.figure(figsize=(8, 6))

    # Ploting averaged values with error bars representing SE
    plt.errorbar(sampled_indices, sampled_values,
                 yerr=sem, fmt='o', capsize=5, label='Averaged Values with SE')

    plt.title('Averaged Values with Error Bars (SE)')
    plt.xlabel('Data Point Index')
    plt.ylabel('Averaged Value')
    plt.legend()
    plt.grid(True)
    plt.tight_layout()
    plt.show()

else:
    print("Data was not loaded successfully. Check the file path and try again.")
