## Basic Structure of Beam Pipeline Code in Python

Apache Beam pipelines in Python can be written in a few different ways. Below is a basic example demonstrating the structure of a Beam pipeline using both the regular method and the method using the `with` keyword.

### Example Pipeline: Reading, Processing, and Writing Data

This example pipeline reads lines of text from an input file, converts each line to uppercase, and writes the results to an output file.

### Method 1: Regular Method

```python
import apache_beam as beam

def run():
    # Create a pipeline using the DirectRunner
    pipeline = beam.Pipeline()

    # Define the pipeline steps
    (pipeline
     | 'Read' >> beam.io.ReadFromText('input.txt')
     | 'Process' >> beam.Map(lambda x: x.upper())
     | 'Write' >> beam.io.WriteToText('output.txt'))

    # Run the pipeline
    pipeline.run().wait_until_finish()

if __name__ == '__main__':
    run()
```

### Method 2: Using the with Keyword
Using the with keyword ensures that the pipeline is properly initialized and finalized, simplifying resource management.

```python
import apache_beam as beam

def run():
    # Create and run the pipeline using the with keyword
    with beam.Pipeline() as pipeline:
        # Define the pipeline steps
        (pipeline
         | 'Read' >> beam.io.ReadFromText('input.txt')
         | 'Process' >> beam.Map(lambda x: x.upper())
         | 'Write' >> beam.io.WriteToText('output.txt'))

if __name__ == '__main__':
    run()
```
