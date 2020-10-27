---
title: Formants and their extraction
date: 2020-10-27 15:26:49
categories:
  - Math
tags:
  - Linguistics
  - Formants
---

N.B. I wrote this article in the process of participating in [Project Spectra](https://www.researchgate.net/publication/344300148_Online_Community-based_Design_of_Free_and_Open_Source_Software_for_Transgender_Voice_Training). We originally envisioned including resonance-related exercises at the time, but due to limitations on our access to professional speech therapist input, knowledge, and implementation we only managed to finish pitch-based exercises.

# What are formants?

> A formant is a concentration of acoustic energy around a particular frequency in the speech wave. There are several formants, each at a different frequency, roughly one in each 1000Hz band for average men. The corresponding range for average women is one formant every 1100Hz. The true range depends on the actual length of the vocal tract. Each formant corresponds to a resonance mode of the vocal tract.

> Seen this way, the sound spectra look like mountain landscapes and the formants appear as peaks, a metaphor that is often used for formants. [12]

> The frequency of the first formant is mostly determined by the height of the tongue body:

    high F1 = low vowel (i.e., high frequency F1 = low tongue body)
    low F1 = high vowel (i.e., low frequency F1 = high tongue body)

> The frequency of the second formant is mostly determined by the frontness/backness of the tongue body:

    high F2 = front vowel
    low F2 = back vowel

https://web.archive.org/web/20190213064736/https://home.cc.umanitoba.ca/~krussll/phonetics/acoustic/formants.html

> F3: The lower of the formant frequency, the rounder shape of the lip e.g. /U/, /uù/, but F3 is not as frequently used as F1 and F2.


Since the 1950s, and even before, attempts have been made to visualize the vowel space by plotting at least F1 and F2 after collecting large corpuses of data. (Keywords to search for: vowel chart, vowel diagram) One such corpus with 1520 samples of American English[1] was collected by Peterson & Barney in 1952. This particular dataset can be found in various open source libraries such as Praat (http://web.archive.org/web/20190831081419/https://raw.githubusercontent.com/praat/praat/master/dwtools/Table_extensions.cpp) or packages in CRAN.

> ..., men, women, and children have vocal tracts of markedly different sizes, so that naturally their formants are different. Yet we identify a child's vowels correctly in spite of this. An /i/ said by a man and an /i/ said by a woman are felt to be "the same sound" and are equated, as far as phonetic quality goes, by the phonetician. On the usual F1/F2 plot they have quite different positions, but on an "articulatory" vowel-diagram they have the same position. Peterson has suggested that a more realistic acoustic diagram is achieved by plotting the ratio of F1 to F3 along the vertical axis and the ratio of F2 to F3 along the horizontal axis, all values being expressed in mels. Then men's, women's and children's "same" vowels are claimed to come out with approximately the same positions.[2]

<!--more -->
## In what ways do formants differ by gender?

An interesting study by Cartei et. al[6] tries to gauge the behavioral aspect of formant production by having 32 men and women (undergraduate students from a university) try to masculinize and feminize their voices.

> Because formant frequencies are negatively correlated with the
length of the vocal tract, male speakers produce lower Fi
values and therefore a formant spacing (ΔF) that is about 15%–20% narrower than in female speakers, which
results in male voices having a more "baritone" timbre.

However, despite the participants' attempts, one telltale sign was the dynamic range of both the fundamental frequency and the formants, especially in Figure 2; note how little both the male and female /æ/ varies from neutral especially in the feminization attempts.
> The effect of sex on F0CV was not significant for vowels, but was significant in the other two tasks, indicating that, overall, men spoke with a narrower dynamic range than women.

This appears to be the case for other languages; the female vowel space appears to be a "scaled-up" and shifted version of the male vowel space, albeit the scaling factor is certainly **not** uniform and **not** a simple function of the vocal tract length.[7]

Another study by Cartei and Reby[8] suggests that preadolescent children of both sexes tend to speak with the same F0, however,

> ... boys speak with lower formants and consequently narrower ΔF than  girls despite the absence of overall differences in vocal tract length  between the two sexes before puberty. This dimorphism has led to the suggestion that pre-pubertal sex differences in ΔF have a behavioural basis (for example boys may round their lips or lower their larynx when  they speak to lengthen their vocal tracts).

Certainly, the vocal tract length already varies from *vowel to vowel* (because as you move your tongue or lips you constrict the volume in your vocal tract in different ways); estimating a speaker's VTL from an arbitrary recording is still an *open problem* and a good solution to this would find applications in areas as wide as forensics (because VTL can be used to extrapolate a person's height and weight.) http://web.archive.org/web/20190901152202/https://www.researchgate.net/post/How_can_I_estimate_a_persons_vocal_tract_length_using_a_recorded_audio_file

# Obtaining formants from a speech sample

Schiel and Zitzelsberger identified the following three main strategies that existing formant estimators use[9]:
> Most algorithms to estimate formant parameters from the recorded speech signal therefore either apply homo-morphic analysis of the spectral envelope (e.g. cepstral analysis followed by a peak-picking strategy), or LPC analysis (Markel & Grey, 1982) to estimate the z-transform followed by a pole- picking strategy, or trained pattern recognition techniques (e.g. support vector machine, random forest or deep learning). The latter requires a training set of labelled formant tracks and is in most cases language dependent, while the former two approaches are inherently language independent and do not require any training material.

One such deep learning strategy implemented by Dissen and Keshet[11] feeds both LPC and cepstral coefficients into a neural network with 3 hidden layers as as regression problem, the output layer of which contains 3 output neurons, continuous in nature which predict F1..3.

Below is a plot of the frequency response of the filter (as in the source-filter model of vocal production) as modeled by LPC coefficients compared with the original spectrum as obtained from a simple FFT transform:

![https://ccrma.stanford.edu/~jos/SpecEnv/LPC_Envelope_Example_Speech.html](https://web.archive.org/web/20190902080951im_/https://ccrma.stanford.edu/~jos/SpecEnv/img40.png)

The first three formants are 700, 1220, 2600.
# Worked Example
Example: Obtain F1, F2, and F3 of [this audio sample](https://github.com/project-spectra/test-app/files/3566711/pooling_recording_project_spectra.zip) of me saying the English word "pooling", in particular the excerpt of the vowel /uː/ (oo) from 00:00:95 to 00:01:00 titled `pooling_transfusion_oo_0_95_1_0.wav`, using the LPC root-finding method.

The code as a single `.m` file is provided [here](https://gist.github.com/Transfusion/2d560696e62f335c741d712b479e127c)

## Results we should expect to get
1. Open up Praat and load the sound sample in.
![](https://user-images.githubusercontent.com/3119646/64277028-f16eac80-cf7b-11e9-8c40-994efb44abef.png)
2. A general guideline in the literature is "one formant in each 1000 Hz band", thus we must capture frequencies up to 5000 Hz to obtain the first 5 formants. This figure is increased by 10% for female voices; hence one formant every 1100 Hz and up to 5500 Hz should be captured. According to the Nyquist theorem, the sample rate should be doubled to become 10000 Hz and 11000 Hz respectively. The literature also recommends downsampling to these values (and perhaps even higher such as 16000 Hz in the case of children); empirically, with the instructions below, certain LPC coefficients are skipped if the algorithm is executed on the full 44100 Hz sampling rate.

3. Try the inbuilt formant extractor in Praat first after selecting `View & Edit`, then `Formant > Formant Listing`.
![](https://user-images.githubusercontent.com/3119646/64282035-13b9f780-cf87-11e9-8e00-f3f3d4865e1a.png)
    ```
    Time_s   F1_Hz   F2_Hz   F3_Hz   F4_Hz
    0.025000   352.892934   796.173876   2903.324760   3507.097425
    ```
    The code behind this is located [here](https://github.com/praat/praat/blob/e453b143ac829786855fa9464486dbd4fad62df0/LPC/Sound_and_LPC_robust.cpp#L202).

4. Let's try to plot the LPC-modelled spectrogram. Note that extracting formants from the LPC coefficients manually (seems) to skip a few steps compared to the `Formant Listing` method, notably `LPC_Sound_to_LPC_robust`, which applies a gaussian window and applies preemphasis.

    1. Select `pooling_transfusion_oo_0_95_1_0` in the `Praat Objects` window and click `Convert > Resample`. Set the `New sampling frequency` as 10000 Hz, then click OK.

    2. In the `Objects` window, select the newly downsampled object and click on `Analyse spectrum > To LPC (autocorrelation)`, then click OK.

    3. The newly created LPC object should be selected. Click on `To Formant`, then with the Formant object selected, click on `Tabulate > List`, then click OK. You should see:

        ```
        time(s)	nformants	F1(Hz)	B1(Hz)	F2(Hz)	B2(Hz)	F3(Hz)	B3(Hz)	F4(Hz)	B4(Hz)	F5(Hz)	B5(Hz)
        0.025000	5	345.716	85.135	791.642	111.987	2814.110	349.209	3487.712	92.460	4335.240	1658.090
        ```

        B refers to the bandwidth, thus the first 3 formants are 345.716, 791.642, and 2814.110, close enough to our benchmark values.

    4. Head back to the `Objects` window and select the LPC object. Click on `To Spectrum (slice)`, then click OK. Select the downsampled sound sample object, click on `Analyse spectrum > To Spectrum.`, then click OK. There should now be two Spectrum objects in the `Objects` window. Click on one of them, then click on `Draw > Draw`; repeat for the other one. The resulting image should be as follows:

    ![](https://user-images.githubusercontent.com/3119646/64308068-ad56c880-cfca-11e9-9dd4-0dda0118e4f7.png)

    5. To interact with the LPC spectrum alone and find the peaks visually, click on the Spectrum object in the `Objects` window, then click `View and Edit`.

## Implementation in MATLAB

```matlab
[snd, originalFs] = audioread('pooling_transfusion_oo_0_95_1_0.wav');
Fs = 10000;

% downsample to 10 KHz
snd = resample(snd, Fs, originalFs);

segmentlen = 100;
noverlap = 90;
NFFT = 4096;
```

Perform preemphasis on the signal because lower frequencies often have disproprotionately higher energy:

```matlab
% warning: preEmphasisFrequency must be below the nyquist frequency!
% http://www.fon.hum.uva.nl/praat/manual/Sound__Filter__pre-emphasis____.html
preEmphasisFrequency = 50; % the default in praat, hz
preEmphasized = zeros(size(x));
alpha = exp(-2.0 * pi * preEmphasisFrequency * (1/Fs) ); 

for i = length(preEmphasized):-1:2
    preEmphasized(i) = snd(i) - alpha * snd(i-1);
end

snd = preEmphasized;
```
Apply a Gaussian window to avoid spurious frequencies where the signal begins and terminates:

```matlab
snd = snd.*gausswin(length(snd));
```

### What does LPC do?
*Linear Prediction* is the process of coming up with a linear model which determines the value of the current sample in a discrete time series based on past/observed values.

Sound is produced by a wave travelling through a medium. To see the actual waveform of me saying oo, try `plot(snd)`; the result should be as follows:

![untitled](https://user-images.githubusercontent.com/3119646/64449991-b2735f00-d113-11e9-8e4c-a31408640a7a.png)

Note the various periodic waves; for instance, every other wave has two "humps" in it and the second hump appears to be of higher amplitude. We can predict the value at any arbitrary X position (time) given the previous samples. 

A **transfer function** when dealing with time series in signal processing (like right now) or control engineering is simply the ratio of the output signal to the input signal.

In the literature, it is common to model the vocal tract's transfer function as an [all-pole filter](https://www.ee.columbia.edu/~dpwe/e4896/lectures/E4896-L06.pdf), reproduced below. A pole is when the response function goes to infinite; i.e. when the denominator of the transfer function is 0. A zero occurs when the numerator is 0. Thus, a response function with a constant in the numerator is all-pole.

<img src="https://user-images.githubusercontent.com/3119646/64478805-7823c380-d1e0-11e9-9739-019198488bbd.png" alt="drawing" width="400"/>

Transfer function of the vocal tract.

The vector `a`, of length `p`, is the coefficients associated with every term of the polynomial, also of order `p`.

Let `Output(z)` be `X(z)`, and `Input(z)` be `E(z)`.

Let `X(z)` be the current sample in the z-domain and `E(z)` be the source in the source-filter model. `X(z) = H(z) * E(z)`.

Cross multiplying the fractions in the transfer function, we get:
```
E(z) = X(z) - X(z) * [term with summation]
X(z) = X(z) * [term with summation] + E(z)
```

![aOw4sW jpg](https://user-images.githubusercontent.com/3119646/64479745-b1166500-d1ed-11e9-9b41-51b6de7ae6be.png)

Bringing this expression back into the time domain by doing the inverse z-transform so we have a concrete expression that we can use to express the current sample in terms of our past samples:

<img src="https://user-images.githubusercontent.com/3119646/64479538-2d5b7900-d1eb-11e9-87e2-8413e9789156.png" alt="drawing" width="500"/>


This is also known as the **time-shifting property** of the z-transform. The summation on line 3 begins at *k* because we must at least have k samples in our array if we want to be able to look backwards by k samples; i.e. it is not logical for `n-k` to be negative.

Substituting back into the expression we get after cross multiplying,
![Exg8yj jpg](https://user-images.githubusercontent.com/3119646/64479635-621c0000-d1ec-11e9-9cf0-9495231d632f.png)

i.e. each sample is simply a weighted sum of the immediate previous `p` samples in this model + what used to be our input impulse.

However, we have our actual audio sample and we want to estimate `a_k`, our coefficients now (which would be the coefficients of the polynomial in the original z-domain), thus `e(n)` takes on the role of the prediction error when we apply linear regression to find `a`. We will skip working out the actual linear regression in this guide since libraries exist to do so after all.

```matlab
[A, err] = lpc(snd,10);
[H, F] = freqz(err^0.5,A,NFFT,Fs);
figure;
plot(F,log(abs(H)));
```
According to [MATLAB documentation](https://web.archive.org/web/20190907201614/https://www.mathworks.com/help/signal/ref/lpc.html), the `lpc` function finds `a` in such a way that

![CH5EST jpg](https://user-images.githubusercontent.com/3119646/64479858-c1c7da80-d1ef-11e9-88af-8ff81808d944.png)

they are negative; thus when plugged into the polynomial above with `z^-k` they become positive.

> Convolution Theorem: Multiplication in the discrete-time domain becomes convolution in the z-domain. Multiplication in the z-domain becomes convolution in the discrete-time domain.

Finding the roots of the polynomial described by `A`, (you may try [this website](https://xrjunque.nom.es/rootfinder.aspx)) which is `x^10-0.990957239467850*x^9-0.125655790125284*x^8-0.838547440244313*x^7 + 1.20775228094351*x^6 + 0.333452550451733*x^5 + 0.0448200046527322*x^4 -0.493766106144003*x^3 -0.409998016009997*x^2+ 0.219683972440823*x + 0.230480465418990 = 0`

(The first item in `A` is 1); we should obtain
```
-0.570431810344407-i*0.787004105407124
-0.570431810344407+i*0.787004105407124
-0.563770157146396-i*0.196261544293191
-0.563770157146396+i*0.196261544293191
-0.164548102245518-i*0.870100929756742
-0.164548102245518+i*0.870100929756742
0.844894632920703-i*0.457672165731046
0.844894632920703+i*0.457672165731046
0.949334056549543-i*0.21047565099229
0.949334056549543+i*0.21047565099229
```

Plotted on the complex plane, these are:

![untitled_4](https://user-images.githubusercontent.com/3119646/64483663-fc099a00-d238-11e9-9e83-f2e7c74a421c.png)

```matlab
rts = roots(A);
rts = rts(imag(rts)>=0); % retain only the roots with positive imaginary component (thus above the horizontal axis in the picture above)
angz = atan2(imag(rts),real(rts));
```
The angles of said points in degrees are:
```matlab
>> rad2deg(angz)

ans =
          12.5007684107254
          28.4440247430048
          100.708953320254
          125.935136252332
          160.805800678623
```

These angles we see here, informally, are how far each of the individual frequency components have "travelled around the unit circle" in a **single sample**. Our sampling rate is now 10000 Hz. The units above are in **radians/sample**, thus we need to multiply them by 10000 before applying the formula for **angular frequency**.

```matlab
[frqs,indices] = sort(angz.*(Fs/(2*pi)));
```

<img src="https://user-images.githubusercontent.com/3119646/64485925-fcb22880-d258-11e9-94c2-31cc0b82194d.png" alt="drawing" width="300"/>

At this point, the `frqs` variable should contain our formants and be quite similar to both our attempts using Praat! They should be:

```matlab
frqs =

          347.243566964593
          790.111798416799
           2797.4709255626
          3498.19822923145
          4466.82779662843
```

### Optional but recommended step
TODO: Explain the distance from the unit circle and how it relates to the **formant bandwidth** in simple terms

Additional filtering/thresholding may be done on the obtained formants.

The bandwidth is basically how platykurtic the formant region is; i.e. a 400 Hz wide swath of sound all around the same amplitude level is more likely to be noise than a resonance of the vocal tract.

```matlab
bw = -1/2*(Fs/(2*pi))*log(abs(rts(indices)));

nn = 1;
for kk = 1:length(frqs)
    if (frqs(kk) > 90 && bw(kk) <400)
        formants(nn) = frqs(kk);
        nn = nn+1;
    end
end
```

### Investigating the model described by A

Previously, before performing `lpc`, we came up with an expression relating the current sample with the immediate previous p samples. Let's eyeball this on a couple arbitrary samples:

```matlab
>> snd(399-10:399)

ans =

      -0.00692307756475205
      -0.00698452989019883
      -0.00393614172085627
      -0.00627761144814771
      -0.00867164003550028
      -0.00575188812920859
      -0.00699546688431311
       -0.0068232860115245
      -0.00352345532564564
      -0.00223809113403957
       0.00107157362766187
```

Let us try to predict the 399th (starting from the 1st) sound sample; the prediction should at least be positive:

```matlab
>> - A(2:end) * flipud(snd(398-9:398))

ans =

      0.000789732959574569
```

Another one:
```matlab
>> snd(199-10:199)

ans =

       -0.0148137512854369
      -0.00909400429482982
       -0.0142895693927139
       -0.0209940327026022
       -0.0126893465686367
       -0.0131553582512722
      -0.00643197461229436
       0.00402941604871497
       0.00987810570587273
        0.0207191216380541
         0.028318966315502

>> - A(2:end) * flipud(snd(198-9:198))

ans =

        0.0270627680148722
```

Note that we do `flipud` because the nearest sound sample, the one before the one we're trying to predict, corresponds to the 1st coefficient in `A` after 1.

# Potential Pitfalls

- > For consonants, there are also antiresonances in the vocal tract at one or more frequencies due to oral constrictions. An antiresonce is the opposite of a resonance, such that the impedence is relatively high rather than low. Consequently, they attenuate or eliminate formants at or near these frequencies, so that they appear weakened or are missing altogether when you look at spectrograms. That is why, for example, it is difficult to see formants below 3000-4000Hz for the two instances of [s] in the spectrogram above. [12]
    - The literature describes some success detecting the nasal consonants n and m because the nasal cavity has its own resonances.
    - Fricatives tend to resemble noise across the spectrum and be much shorter in duration.

- F1 and F2 alone may not be sufficient to represent all the cardinal vowels in certain languages.

    - > In languages that contrast front vs. mid, round vs. unrounded vowels, F3 plays a critical role. In French, for example, F1 and F2  for /i/ and /y/ can be similar for some speakers.[3]
    - Vaissière proposes various ways to aggregate F2 and above into a single dimension.
# Future Ideas

## Shifting the formants of a recorded voice sample
This study[13] involving the perception of masculinized and feminized versions of male and female voices leverages the
> Pitch-Synchronous Overlap Add (PSOLA) algorithm in Praat version 5.2.15. Pitch was raised (feminized) or lowered (masculinized) by 10% from baseline while holding formants constant. Likewise formants were raised (feminized) or lowered (masculinized) by 10% from baseline while holding pitch constant. This process created 12 pairs of voices (6 male and 6 female) that differed in pitch and 12 pairs of voices that differed in formants (6 male and 6 female). Following these manipulations, we amplitude normalized the sound pressure level of all voices to 70 decibels using the root mean squared method.

It would be interesting to see how the mapping is done from the masculine to female vowel space.

Informally, various commercial music VSTs such as Little AlterBoy by SoundToys and MAutoPitch by MeldaProduction and Melodyne by Celemony claim to manipulate formants.

# Related Topics

## Synthesis of voice based on the extracted formants

We can feed the formants back into vocal synthesizers based on the source-filter model.

One such vocal synthesizer by Clo Yun-Hee Dufour can be found [here](https://synth.transvoice.info); try it with the frequencies and bandwidths found above!

## Estimation of the vocal tract length

Assuming a neutral vocal tract,
>   Fn = (2n – 1)c/4L;
Where n is an integer, L is the length of the tube and c is the speed of sound (about 35,000 cm/sec).

http://web.archive.org/web/20190908145916/https://www.researchgate.net/post/How_can_I_estimate_a_persons_vocal_tract_length_using_a_recorded_audio_file

A worked example can be found here on the 2nd page: http://web.archive.org/web/20190908152547/https://web.stanford.edu/class/linguist205/index_files/Handout%206%20-%20Vowel%20acoustics.pdf

A Praat script implementing this formula can be found here: http://www.praatvocaltoolkit.com/calculate-vocal-tract-length.html

A problematic assumption is that the vocal tract is completely neutral and has resonances in a 1:3:5:... ratio, e.g. 500 Hz, 1500 Hz, 2500 Hz, ...

n is the frequency of the nth formant.

# Corpuses of Data
[**VTR Formants Database**](https://web.archive.org/web/20180915094923/http://www.seas.ucla.edu/spapl/VTRFormants.html):

> ...a database for manually labeled vocal-tract-resonance (or formant)
trajectories... The database contains a representative subset of the TIMIT corpus with respect to speaker, gender, dialect and phonetic context, with a total of 538 sentences.

# References
[1] [G. E. Peterson and H. L. Barney, “Control Methods Used in a Study of the Vowels,” J. Acoust. Soc. Am., 1952.](https://web.archive.org/web/20190227220201/https://pdfs.semanticscholar.org/970d/43f4f3bb68bd11cd3e16bba758287a3ee9e1.pdf)

[2] [WELLS, J. C. (1962). A Study of the Formants of the Pure Vowels of British English. MA dissertation,University College London.](https://web.archive.org/web/20171210010051/http://www.phon.ucl.ac.uk/home/wells/formants/preldis.htm)

[3] [J. Vaissière, “on the Acoustic and Perceptual Characterization of Reference Vowels in a Cross-Language Perspective,” 17th Int. Congr. Phonetic Sci. (ICPhS XVII), 2011.](https://web.archive.org/web/20181103192130/https://halshs.archives-ouvertes.fr/halshs-00676266/document)

[6] [V. Cartei, H. W. Cowles, and D. Reby, “Spontaneous voice gender imitation abilities in adult speakers,” PLoS One, 2012.](https://web.archive.org/web/20190505222650/https://journals.plos.org/plosone/article/file?id=10.1371/journal.pone.0031353&type=printable)

[7] [R. L. Diehl, B. Lindblom, K. A. Hoemeke, and R. P. Fahey, “On explaining certain male-female differences in the phonetic realization of vowel categories,” J. Phon., 1996.](https://web.archive.org/web/20190901125923/https://pdf.sciencedirectassets.com/272464/1-s2.0-S0095447000X00241/1-s2.0-S009544709690011X/main.pdf?X-Amz-Security-Token=AgoJb3JpZ2luX2VjECwaCXVzLWVhc3QtMSJHMEUCIQDTWfHc2yMMtEoCr8rRUxtBCE5y4xt27ZwXMGGmnCuZRgIgWxa3Mz4nfegxeZEoWMXNNi91bjXrARlapbigm5RUIXgq4wMI1f%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARACGgwwNTkwMDM1NDY4NjUiDJ7TIWvS9VtWlqwW7Cq3A8f8A9pwsUQw3BZH5%2FRgGZ5unoMNkTFMQwDV%2BMbNA3fv7F72iTn0b5JSOS5x%2Fag7xqFRaXzdB9dHcQA1biP3O%2FQv0fn6lji99GXBJ3kjUUPvR2MlOTEPQ%2FqdJfWSx%2F8KHzBXy%2FzyyfW3SCa%2BrDEEwVWYnhtqbdQMv76LhiwesbGzPtCbVHUASzm6DXn6d2qH8c5BcMTuh%2BaqjyjCW%2BLYeitx3XWWAeY%2Btn1Fi4qz6IcuQxFGUJ68BVDx3txJRI2LhlrVMGLmEPQK%2F6wR%2BLMQEGgHc6pZmHFxqOT%2Ft8HIv8i0wo9%2BD7sRdiQSDzO53UBx6CAikOKYVWObTYfGmqw6yVnOMwuarDZoXrGivPhb1XKYcn74e3nnRuOGqfUCHmmih3EaSgN1wNv0HFLZjJ%2FI7vKC81REtsaYp%2FAsMUVSpKO%2FcpoLRirU2mxbsUnQ%2F%2F2krieI19TRNpMrOGif%2BjxsgjRcZKzJvQWeg0ahAT05TTNQgT92qF1r8h8kLV6B6Kx3UrXczSkw5XvZbyQG5yxwT4bWlzqoA6gTawOrvYkPV9YKuBt4fSX5rur1JnbO1yVymLjVPFjX1hIwtdeu6wU6tAG%2BE8KPWkQL9XCxoS1Ulcbf1Dc1X3ArC1j9ZyJYaD9ixz3ZCecI%2BiTMrt%2BW3CzOS%2FBqwNr4BC2f4qj6IGGGWGalwB0TPVqNc8AVbc6WHkiqX0TnSESjAK5i0GU7PLqfd0ZgfiMO9oq7V%2FA67Bm22%2FmiIkZiHEshj%2B462uBNi%2FCtgt6TwT8lunFdU3hOJ6uU49V68McoCkscWQKMrZyd5u%2B9hAYEFyrmeqTJsg62DIfpxpnEqME%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20190901T125856Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYZNPOJJAE%2F20190901%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=0b4698809da53fe368451f4b2410675325317764fb53417512c25758f035636c&hash=488282aea8fe6a9183cd74bab66acc40590cd21b965b8d4f86af76fd85b44969&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S009544709690011X&tid=spdf-ce2e3243-1db9-4551-a291-2b5de31c8fe8&sid=69e2a20c3392e0485c489887eb6845b8225cgxrqb&type=client)

[8] [V. Cartei and D. Reby, “Effect of formant frequency spacing on perceived gender in pre-pubertal children’s voices,” PLoS One, 2013.](https://web.archive.org/web/20190504094702/https://journals.plos.org/plosone/article/file?id=10.1371/journal.pone.0081022&type=printable)

[9] [F. Schiel and T. Zitzelsberger, “Evaluation of automatic formant trackers,” in LREC 2018 - 11th International Conference on Language Resources and Evaluation, 2019.](https://web.archive.org/web/20190901155003/https://www.aclweb.org/anthology/L18-1449)

[10] [Kim, Chanwoo & Sung, Wonyong. (2001). Vowel Pronunciation Accuracy Checking System Based on Phoneme Segmentation and Formants Extraction.](https://web.archive.org/web/20190901155934/https://pdfs.semanticscholar.org/14a0/8c3e1858dc04bd5ea12fdd1032036e914bc6.pdf)

[11] [Y. Dissen and J. Keshet, “Formant estimation and tracking using deep learning,” in Proceedings of the Annual Conference of the International Speech Communication Association, INTERSPEECH, 2016.](https://web.archive.org/web/20190902120628/http://u.cs.biu.ac.il/~jkeshet/papers/DissenKe16.pdf)

[12] [S. Wood, "Praat for Beginners", accessed 2019.](http://web.archive.org/web/20190204033820/https://person2.sol.lu.se/SidneyWood/praate/whatform.html)

[13] [M. Kandrik et al., “Are men’s perceptions of sexually dimorphic vocal characteristics related to their testosterone levels?,” PLoS One, 2016.](http://web.archive.org/web/20190908185815/https://journals.plos.org/plosone/article/file?id=10.1371/journal.pone.0166855&type=printable)