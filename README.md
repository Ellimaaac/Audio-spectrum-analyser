# Audio-spectrum-analyser


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

```matlab
% Informations générales sur la musique
audioInfo = audioinfo(fullfile(path, file))
fe = audioInfo.SampleRate % fréquence d'échantillonnage
Dobs = 0.5; %Durée d'observation (s)
te = 0:1/fe:Dobs-1/fe; % période d'échantillonnage
% Vecteur temps
[audio,~]=audioread(fullfile(path, file));
%Tanspose la matrice pour avoir le temps le long des colonnes
audio = audio.';
