voicerecognition
================

voice recognition

mkdir build

cp mylm.lm build/

cp mydict.dic build/

cd build

cmake ..

make

./pcro

Functionality:

>As soon as ui opens up,select detect face,it will detect face after a while(5-10 seconds) if not repeat the process untill correct face is detected.
>Give some name in edit box provided below and select save.
>select recognize face,now system try to recognize you,and after a while system starts recognizing the voice,select  parameters to generate waveform in the order wave-type,wave freqency,wave voltage,wave duration one by one by observing the terminal.
 
An example of voice command sequence look similar to this>>>> 'sine' > 'next' > 'one' > 'zero' > 'zero' > 'zero' > 'next' > 'three' > 'next' > 'two' > 'next' > 'generate'
  
In case voice recognized wrongly you can optionally say 'cancel',inorder to repeat and continue to selecting parameters.

After 'generate' utterance you should see waveform plotted displayed on ui and also hear sound corresponding to waveform,optionally you can connect headphone jack to any circuit/cro to see the waveform generated while sound is playing.

You can altogether discard voice and face recognition functionality and use as signal generator alone by mannually setting parameters and selecting play pushbutton.

Make-sure
You have opencv,sphinx-base,sphinx-training,pocketsphinx Qt installed in your system And you have mylm.lm,mydict.dic files in the build directory,where you have pcro binary file or you can have other language model if you want.
