# DREAM_PD
## Parkinsons Disease Digital Biomarker DREAM Challenge - Subchallenge 2 (L-Dopa)

We use an anomaly detection approach based on a one-class SVM trained on a set of time and frequency-domain features to estimate the severity of bradykinesia, dyskinesia and tremor.
### Background/Introduction

The main difficulties with automatic symptom scoring from the 3 challenges datasets [1] are: 1) the high class imbalance between presence and absence of symptoms (or between level of severities for tremor); 2) the low number of subjects in the dataset; and 3) the fact that metadata of subjects alone can already predict well the subject scores. This makes the classification problem very difficult, especially in terms of generalization to unseen subject.
Here we use a semi-supervised learning approach, such that a model is fitted to subjects with no symptoms (score of 0); then a new subjects is given a distance score (probability) from the healthy (no-symptom) model. This approach is inspired by our previous work on clinical scoring using Naive Bayes surprise for walking skills [2].

### Methods
We compute a set of 35 time and frequency-domain features from windowed accelerometer recordings of 5 second-length. These features include: energy of the signal, the statistical moments of the raw acceleration data, jerk and power spectral density (PSD); cross-correlation for each axis, as well as the dominant PSD frequency and its power relative to the total. These features were used in previous studies and proved successful [3]. We then train a one-class SVM with an RBF kernel [4] on the windows with a score of 0 for the corresponding symptom. This approach learns a decision function for novelty detection that classifies new data as similar or different to the training set. The final feature matrix submitted for each challenge is composed of the metadata information (session, side, etc.), the task duration and the surprise score. We take the minimum (most different from 0) surprise score for a given recording. We used this approach for all 3 challenges (bradykinesia, dyskinesia, tremor).

### References
[1]Parkinson's Disease Digital Biomarker DREAM Challenge (syn8717496)

[2]Lonini, L., Shawen, N., Scanlan, K., Rymer, W. Z., Kording, K. P., & Jayaraman, A. (2016). Accelerometry-enabled measurement of walking performance with a robotic exoskeleton: a pilot study. Journal of neuroengineering and rehabilitation, 13(1), 35.

[3]Patel, Shyamal, et al. "Monitoring motor fluctuations in patients with Parkinson's disease using wearable sensors." IEEE transactions on information technology in biomedicine 13.6 (2009): 864-873.

[4]One Class SVM - SKLearn Documentation http://scikit-learn.org/stable/auto_examples/svm/plot_oneclass.html#sphx-glr-auto-examples-svm-plot-oneclass-py

[5] Džeroski, S., & Ženko, B. (2004). Is combining classifiers with stacking better than selecting the best one?. Machine learning, 54(3), 255-273.
Chicago
