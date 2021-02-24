
# Simulation set synthesis

## 1. The simulation rirs
Parameter and path in configuration `challenge_rirgenerator.py` file

```bash 
export LD_LIBRARY_PATH=/path/to/ConferencingSpeech2021/simulation/:$LD_LIBRARY_PATH
python ./challenge_rirgenerator.py
```
Please make sure that your Python version is higher than 3.6. If you use the supplied RIR, this step is not required.

## 2. Prepare speech and noise sets
### 2.1 Download the data
speech data:

[aishell-1](http://openslr.org/33/) 

[aishell-3](http://openslr.org/93/)

[librispeech-360](http://openslr.org/12/)

[VCTK](https://datashare.ed.ac.uk/handle/10283/2651)


noise data: 

[MUSAN](http://openslr.org/17/)

[Audioset](https://github.com/marc-moreaux/audioset_raw)

### 2.2 Generate the list file and partition the training and checksum sets

Configure the path to several datasets in `./prepare.sh`

```bash
bash ./prepare.sh
```


## 3. Generate the data

Configure using the supplied parameters

> Attention to the data/[dev | train]_[linear|circle]_simu_mix.config . In the config file path should be replaced with the corresponding path. Generate these config file as follow.

```bash 
# training set of linear mic array
python mix_wav.py --clean_wav_list=./data/train_clean.lst --noise_wav_list=./data/train_noise.lst --rir_wav_list=./data/train_linear_rir.lst --mix_config_path=./data/train_linear_simu_mix.config --save_dir=./data/wavs/train/simu_linear --chunk_len=4 --generate_config=True

# dev set of linear mic array 
python mix_wav.py --clean_wav_list=./data/dev_clean.lst --noise_wav_list=./data/dev_noise.lst --rir_wav_list=./data/dev_linear_rir.lst --mix_config_path=./data/dev_linear_simu_mix.config --save_dir=./data/wavs/dev/simu_linear --chunk_len=6 --generate_config=True
``` 

the output of save_dir will include three folder:

```bash
mix\ # speech with reverberation and noise
noreverb_ref\ # clean speech with  early reverberation (default 50ms)
reverb_ref\ # clean speech with reverberation
```
