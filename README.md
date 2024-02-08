# Audio-spectrum-analyser


Caractéristique du signal audio
```matlab
% Sélection du fichier audio
[file, path] = uigetfile(...
    {'*.wav;*.flac;*.mp3;*.mp4', 'Fichiers audio (*.wav;*.flac;*.mp3;*.mp4)'},...
    'Selectionnez un fichier audio');
if file == 0
    return;
end
```matlab
