# AI Music Generation with MusicGen
## Introduction
This project harnesses the power of artificial intelligence to generate music through textual descriptions using the MusicGen model from the AudioCraft package. Developed by Meta AI, the MusicGen model has been pre-trained to understand intricate relationships between text prompts and musical audio.


## Table of the Content
* Dependencies
* Installation
* Usage
    * Importing dependencies
    * Loading the Pre-trained Model
    * Configuring Generation Parameters
    * User Interface
    * Generating Music
    * Displaying the UI
* Examples and Experimentation
* Next Steps

## Installation
Install the required dependencies using the following command:

```
pip install torchaudio audiocraft ipywidgets
```

## Usage
### Importing the dependencies and loading the Pre-trained Model

```
import torchaudio
from IPython.display import Audio
from ipywidgets import Textarea, Button
import audiocraft
from audiocraft.models import MusicGen

# Load the pre-trained MusicGen model
model = MusicGen.get_pretrained('facebook/musicgen-small')

```
### Configuring Generation Parameters
```
# Set the duration of the music
model.set_generation_params(duration=8)

```

### User Interface
Create a text area for multiline input and a button to generate music:
```
# Create a text area and a button
description = Textarea(value='', placeholder='Give a music prompt', disabled=False, rows=4)
generate_button = Button(description="Generate Tune")

```

### Generating Music

```
# Function to generate music as prompted
def generate_tune(event):
    results = model.generate([description.value])
    sampling_rate =  model.sample_rate
    display(Audio(results[0].numpy(), rate=sampling_rate))

# Creating a click event on the button
generate_button.on_click(generate_tune)

```

### Displaying the UI

```
# Display the UI items
display(description)
display(generate_button)

```
## Examples and Experimentation
Experiment with different prompts to generate music:

```
# Short prompt
results_short = model.generate(['rock song'])
sampling_rate_short =  model.sample_rate
Audio(results_short[0].numpy(), rate=sampling_rate_short)

# Longer, descriptive prompt
results_long = model.generate(['upbeat rock song with guitar solo'])
sampling_rate_long =  model.sample_rate
Audio(results_long[0].numpy(), rate=sampling_rate_long)

```

## Next Steps
Explore further by comparing the outputs from different models:

```
model1 = MusicGen.get_pretrained('facebook/musicgen-small')
# [Configure model1 parameters]

results_model1 = model1.generate(['classic rock song'])
sampling_rate_model1 =  model1.sample_rate
Audio(results_model1[0].numpy(), rate=sampling_rate_model1)

model2 = MusicGen.get_pretrained('facebook/musicgen-medium')
# [Configure model2 parameters]

results_model2 = model2.generate(['classic rock song'])
sampling_rate_model2 =  model2.sample_rate
Audio(results_model2[0].numpy(), rate=sampling_rate_model2)

```
