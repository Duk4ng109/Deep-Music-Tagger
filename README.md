# Deep Music Classifier

## Note

I plan to finish and upgrade this project as soon as possible. Still I haven't run any complete training procedure, but after I do and verify it, the plan is to use this specific classifier for music generation based on genre, which, to the best of my knowledge, still hasn't been done.

If you need assistance running the project or have a question, please email me on kristijan.bartol@gmail.com

## About

The ideal goal of this project is to be able to say "This part of the song has the elements of jazz, progressive rock and a bit of grunge.". This could be possible to achieve defining the problem as multi-output classification.

Deep model is based on [Dec 2016.] [Convolutional Recurrent Neural Networks for Music Classification](https://arxiv.org/abs/1609.04243) (Keunwoo Choi, George Fazekas, Mark Sandler, Kyunghyun Cho) [1], i.e. using convolutional recurrent neural network deep model for multi-output classification task (tagging each music piece using a subset of labels).

## Prerequisite

To be able to run all parts of this project, you will need the following additional Python packages (recommended is Python 3.6):

- **keras** - build and train the high-level model
- **librosa** - extract mel-spectrograms
- **pandas** - analyze FMA metadata
- **numpy** - efficiently work with linear algebra operations
- **tensorflow** (GPU recommended) - modify keras backend
- **matplotlib** - plot various graphs and use it extract librosa spectrograms

## Input features

[Mel-spectrograms](https://en.wikipedia.org/wiki/Mel_scale) are extracted from .mp3s and used as model inputs. An example of such a spectrogram is: ![Mel-spectrogram example](https://github.com/kristijanbartol/Deep-Music-Tagger/blob/master/out/graphs/plot.png)

However, when generating images for the model, image is generated a bit differently - spectrogram values matrix is dumped into an image in grayscale. Information is preserved this way and there is only one input layer for convolution instead of three. An example of such an image is: ![Grayscale spectrogram example](https://github.com/kristijanbartol/Deep-Music-Tagger/blob/master/out/graphs/106462.png)

Other spectrograms could also be used as described and compared in detail in [5]. In this work, except mel-spectrograms, raw audio input will also be tested [6].

## Data

Using [FMA dataset (A Dataset For Music Analysis)](https://github.com/mdeff/fma) [2]. It is a collection of freely available MP3s (under Creative Commons license) most convenient for research projects and (currently) only publicly available music dataset of a kind.
Top 16 genres distribution is shown in the following histogram: ![Genres histogram](https://github.com/kristijanbartol/Deep-Music-Tagger/blob/master/out/graphs/genre_top.png)

## Usage

1. take a look at and download [FMA dataset metadata](https://os.unil.cloud.switch.ch/fma/fma_metadata.zip) (342 MiB). For more details, check [this repo](https://github.com/mdeff/fma).

2. Then download [small](https://os.unil.cloud.switch.ch/fma/fma_small.zip) or [medium](https://os.unil.cloud.switch.ch/fma/fma_medium.zip); try with smaller versions first to set things up and then switch to [large](https://os.unil.cloud.switch.ch/fma/fma_large.zip). I won't use [full](https://os.unil.cloud.switch.ch/fma/fma_full.zip) version as input images then have various sizes and it's anyways to large for my computing resources plus I believe there is more than enough information in 30s trimmed tracks.

3. Extract mel-spectrograms from mp3s running ![mel-spec.py](https://github.com/kristijanbartol/Deep-Music-Tagger/blob/master/src/mel-spec.py) as main module.

4. Generate relevant metadata running ![metadata.py](https://github.com/kristijanbartol/Deep-Music-Tagger/blob/master/src/metadata.py) as main module.

5. Run ![train.py](https://github.com/kristijanbartol/Deep-Music-Tagger/blob/master/src/train.py) to build, compile and train a keras model (CRNN architecture mentioned above).

Project structure:

* data/
	* fma_{size}/
		* 000/
		* 001/
	* fma_metadata/
		* genres.csv
		* tracks.csv
* in/
	* mel-specs/
		* 000/
		* 001/
	* metadata/
		* test.csv
		* train.csv
		* valid.csv
* out/
	* graphs/
	* logs/
* src/
	* main.py
	* mel-spec.py
	* metadata.py
	* model.py
	* utility.py
	
## Results

I still didn't run the whole training process...

## CrowdAI competition (music genre classification - 16 classes)

Source code for this project also contains separate folder for [CrowdAI competition](https://www.crowdai.org/challenges/www-2018-challenge-learning-to-recognize-musical-genre). Main focus of this project in the next 60 days will be gaining better position on the leaderboard.

## Relevant literature

[1] [CRNN for Music Classification](https://arxiv.org/abs/1609.04243)

[2] [FMA: A Dataset For Music Analysis](https://arxiv.org/abs/1612.01840)

[3] [Music Information Retrival (origin of "MIR", Downie)](http://www.music.mcgill.ca/~ich/classes/mumt611_08/downie_mir_arist37.pdf)

[4] [A Tutorial on Deep Learning for Music Information Retrieval](https://arxiv.org/pdf/1709.04396.pdf)

[5] [Comparison on Audio Signal Preprocessing Methods for Deep Neural Networks on Music Tagging](https://arxiv.org/pdf/1709.01922.pdf)

[6] [End-to-end learning for music audio tagging at scale (1D convolution)](https://arxiv.org/pdf/1711.02520.pdf)

For broader references on music information retrieval, check https://github.com/ybayle/awesome-deep-learning-music.
