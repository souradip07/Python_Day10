# Python_Day10
#Example Code for Logging Sensor Data:
import time

def log_sensor_data(filename, data):
    """
    Log sensor data into a text file.

    Parameters:
    filename (str): The name of the file to log data into.
    data (list): A list of sensor readings.

    Returns:
    None
    """
    with open(filename, 'a') as file:
        timestamp = time.strftime("%Y-%m-%d %H:%M:%S")
        for reading in data:
            file.write(f"{timestamp} - {reading}\n")
        print(f"Data logged to {filename}")

# Example usage:
sensor_data = [23.5, 24.1, 22.8, 23.9]  # Simulated sensor readings
log_sensor_data('sensor_log.txt', sensor_data)

#Example Code for Log Analyzer:
def analyze_log(filename):
    """
    Analyze sensor log data from a text file.

    Parameters:
    filename (str): The name of the log file to analyze.

    Returns:
    dict: A dictionary containing the average, maximum, and minimum sensor readings.
    """
    readings = []
    with open(filename, 'r') as file:
        for line in file:
            try:
                reading = float(line.strip().split('-')[-1])
                readings.append(reading)
            except ValueError:
                continue
    
    if readings:
        analysis = {
            'average': sum(readings) / len(readings),
            'max': max(readings),
            'min': min(readings)
        }
    else:
        analysis = {
            'average': None,
            'max': None,
            'min': None
        }
    
    return analysis

# Example usage:
log_file = 'sensor_log.txt'
results = analyze_log(log_file)
print(f"Average reading: {results['average']}")
print(f"Maximum reading: {results['max']}")
print(f"Minimum reading: {results['min']}")
