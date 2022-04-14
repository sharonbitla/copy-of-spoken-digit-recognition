# copy-of-spoken-digit-recognition
A simple audio/speech dataset consisting of recordings of spoken digits in wav files at 8kHz. The recordings are trimmed so that they have near minimal silence at the beginnings and ends.

FSDD is an open dataset, which means it will grow over time as data is contributed. In order to enable reproducibility and accurate citation the dataset is versioned using Zenodo DOI as well as git tags.

Current status
6 speakers
3,000 recordings (50 of each digit per speaker)
English pronunciations
Organization
Files are named in the following format: {digitLabel}_{speakerName}_{index}.wav Example: 7_jackson_32.wav

How to use with Hub
A simple way of using this dataset is with Activeloop's python package Hub!

First, run pip install hub (or pip3 install hub).

import hub
ds = hub.load("hub://activeloop/spoken_mnist")

# check out the first spectrogram, it's label, and who spoke it!
import matplotlib.pyplot as plt
plt.imshow(ds.spectrograms[0].numpy())
plt.title(f"{ds.speakers[0].data()} spoke {ds.labels[0].numpy()}")
plt.show()

# train a model in pytorch
for sample in ds.pytorch():
    # ... model code here ...

# train a model in tensorflow
for sample in ds.tensorflow():
    # ... model code here ...
available tensors can be shown by printing dataset:

print(ds)
# prints: Dataset(path='hub://activeloop/spoken_mnist', tensors=['spectrograms', 'labels', 'audio', 'speakers'])
For more information, check out the hub documentation.

Contributions
Please contribute your homemade recordings. All recordings should be mono 8kHz wav files and be trimmed to have minimal silence. Don't forget to update metadata.py with the speaker meta-data.

To add your data, follow the recording instructions in acquire_data/say_numbers_prompt.py and then run split_and_label_numbers.py to make your files.

Metadata
metadata.py contains meta-data regarding the speakers gender and accents.

Included utilities
trimmer.py Trims silences at beginning and end of an audio file. Splits an audio file into multiple audio files by periods of silence.

fsdd.py A simple class that provides an easy to use API to access the data.

spectogramer.py Used for creating spectrograms of the audio data. Spectrograms are often a useful pre-processing step.

Usage
The test set officially consists of the first 10% of the recordings. Recordings numbered 0-4 (inclusive) are in the test and 5-49 are in the training set.

Made with FSDD
Did you use FSDD in a paper, project or app? Add it here!

https://github.com/Jakobovski/decoupled-multimodal-learning/
https://adhishthite.github.io/sound-mnist/ by Adhish Thite
https://github.com/eonu/torch-fsdd/ - A simple PyTorch data loader for the dataset by Edwin Onuonga
https://proglearn.neurodata.io/ by NeuroData
https://neurodata.io/df_dn/ by NeuroData
External tools
Tensorflow https://www.tensorflow.org/datasets/catalog/spoken_digit
C#/.NET. The FSDD dataset can be used in .NET applications using the FreeSpokenDigitsDataset class included withing the Accord.NET Framework
https://colab.research.google.com/drive/1AINLv7N9tiwdZCNrloVoCgK_W9zNF3Im?usp=sharing code
