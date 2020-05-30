# JASA-Reverberation
Automatic classification based on the perceived level of reverberation.

The codes will be released here and could be cloned by others when the corresponding paper is accepted for publication. 

# MATLAB Reverb model
This repository is contained a full version of the timbral reverb model. For instruction on installing and using this, please see the following sections!

# Phyton Implementation
The python implementation of the timbral_reverb model is a cutdown version of the full MATLAB and Weka implementation.
This release contains a classification model based from a logistic regression. Therefore, the clip_output parameter does not affect this model.

The timbral_reverb function can be called from the timbral_models package. The function should be given a string that is the path and filename of an audio file. For example:

import timbral_models
fname = '/Documents/Music/TestAudio.wav'
reverb = timbral_models . timbral_reverb (fname)

This will return the estimated classification of the audio file as either 0 (indicating the file does not
sound reverberant), or 1 (indicating that the file sounds reverberant).

# Matlab and Weka Implementation
The full version of the timbral_reverb model is implemented with feature extraction in MATLAB and modelling in Weka. The model is implemented as a classification model categorising the sound files into ‘does not sound reverberant’ and sounds ‘reverberant’ categories. The current model better fits with subjective ratings of the perceived level of reverberation compared to previous implementations and the python distribution version.
New features have been extracted from the audio files to predict the perceived level of reverberance. One of extracted features is RT60. The new approach for extracting RT60 is based on blind estimation, meaning that it uses an audio signal as an input, rather than a room
impulse response. This approach is based on the Laplacian model. This is the algorithm the python distribution is based on.

In addition to RT60, the following features are also extracted and combined as an input for the
machine learning modelling approaches:

· Level of foreground stream
· Level of background stream
· Interaural time difference (ITD) fluctuation in the foreground
· ITD fluctuation in the background
· Level of the low-frequency part of the spectrum
· Reverberance
· Clarity
· Apparent source width
· Listener Envelopment

We propose a method for derivation of signal based measures aiming at predicting aspects of room acoustic perception from content specific signal representations produced by a nonlinear model of the human auditory system. This approach simulates multiple aspects of human hearing to resemble human auditory perception.

The reverb model can be run by running the script Reverb_AC_SS_V4 . In this script, several parameters need to be changed prior to execution: the path to the audio files (Line 5); the filename and location to save the output .arff file containing the extracted features (line 8); location of the “.arff” file which contains features of test audio files; the location where Weka is installed (Line 39)); and finally the location and name of the trained reverberation model (line 40). For example:

Run Reverb_AC_SS_V1.m
Line 5: cd( '\\surrey.ac.uk/audiofiles\' ); % location of the audio files
Line 8: fid = fopen( 'ExtractedFeatures.txt' , 'w' ); % file name for storing extracted
features
Line 39: cd( 'C:\Program Files\Weka-3-8' ); % location of Weka installation
Line 40: -l Logistic_classifier_Weka_D5.6.model -T
C:\Users\Fred\Desktop\temp\outputfile.arff % doc command for computing model

By running the main script an explorer will be opened in the specified audio file location (the directory defined at line 5 of the main script). The selected audio files (multiple audio files can be selected simultaneously) will then be analysed.
Extracted features for the selected audio files will be stored in the comma separated format and in a single “.arff” file, specified in line 8. Extracted features are then automatically aligned and reformatted for use in Weka. By running the main MATLAB script the “.arff” file is generated for all the selected audio test files automatically.

To identify the prediction output, two class labels were defined during the training phase: labelled with L or H. These labels are came from the human listening tests, in which L means the audio file has low level of reverberation and H means high level. The Reverberation model is trained using 420 audio files from multiple source types, and simple logistic classifier (Weka logistic classifier with the default predefined parameters) is used for modelling. The pre-trained reverberation model and generated “.arff” files are then used by Weka to estimate the reverberation class. Weka could be used via its own graphic interface or from the Command Prompt environment. In this report, to make it simple for evaluation, the Weka prediction is integrated in the MATLAB script.
