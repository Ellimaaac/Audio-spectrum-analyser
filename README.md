# Audio-spectrum-analyser

This MATLAB script allows you to perform a complete analysis of an audio file, including the extraction of general information about the music, the temporal and frequency evolution of the audio, the representation of the frequency spectrum, the 3D visualisation of the spectrum, the creation of a spectrogram, the analysis of the temporal dynamics, the detection of sound events, the comparison with a reference signal, and the visualisation of frequency peaks.

## How to use it
1. Select an audio file to analyse.
2. Run the MATLAB script.
3. View the results of the audio analysis.

# Script content
The script consists of the following sections:

## 1. To select a local audio file

```matlab
% Sélection du fichier audio
[file, path] = uigetfile(...
    {'*.wav;*.flac;*.mp3;*.mp4', 'Fichiers audio (*.wav;*.flac;*.mp3;*.mp4)'},...
    'Selectionnez un fichier audio');
if file == 0
    return;
end
```
## 2. To select the sampling frequency
```matlab
% Informations générales sur la musique
audioInfo = audioinfo(fullfile(path, file));
fe = audioInfo.SampleRate; % fréquence d'échantillonnage
Dobs = 0.5; %Durée d'observation (s)
te = 0:1/fe:Dobs-1/fe; % période d'échantillonnage
```

## 3. Time and frequency evolution of audio
```
% Vecteur temps
[audio,~]=audioread(fullfile(path, file));
%Tanspose la matrice pour avoir le temps le long des colonnes
audio = audio.';

% Evolution de l'audio en temporelle et fréquentielle
%Axe temporel
t = (0:size(audio,2)-1)/fe;
%Axe fréquentiel
f=linspace(0,fe,size(audio,2));
%Magnitude TF(audio)
TF_audio =abs(fft(audio,[], 2));
```
## 4. Advanced analysis
```
% Représentation en 3D du spectre
TF_audio_dB = 20*log10(TF_audio);
TF_audio_dB = TF_audio_dB';

% Sous-échantillonnage des vecteurs t et f
subsample_factor = 10; % Facteur de sous-échantillonnage
t_subsampled = t(1:subsample_factor:end);
f_subsampled = f(1:subsample_factor:end);

% Création de la grille de coordonnées
[T, F] = meshgrid(t_subsampled, f_subsampled);

% Représentation du spectre en 3D
figure;
surf(T, F, TF_audio_dB);
xlabel('Temps (s)');
ylabel('Fréquence (Hz)');
zlabel('Magnitude (dB)');
title('Spectre 3D de l''audio');
```
Includes advanced features such as 3D representation of the spectrum, creation of a spectrogram, analysis of temporal dynamics, detection of sound events, comparison with a reference signal and visualisation of frequency peaks.
