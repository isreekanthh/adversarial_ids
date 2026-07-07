
# How I Built an AI-Powered Attack That Made an IDS Completely Blind

## Introduction
- What is an IDS and why ML-based IDS is becoming standard
- The hidden assumption: ML models are robust by default
- What adversarial examples are in plain English

## The Target: Building the IDS
- NSL-KDD dataset overview
- Random Forest classifier — why it's used in real SOCs
- Baseline results: 77.31% accuracy, 62% attack recall

## The Attack: Making the IDS Blind
- What FGSM is and how it works conceptually
- The critical constraint problem — you can't just add random noise
- Results: 100% evasion at epsilon=0.05
- What features FGSM targeted and why that makes security sense

## The Analysis: Understanding What Happened
- Why confidence dropped 0.6667 but AUC barely moved
- The surgical vs global attack distinction
- What this means for real SOC environments

## The Defense: Fighting Back
- Feature squeezing — why it failed
- Adversarial training — why it worked
- The accuracy-robustness tradeoff (0.92% cost for 58% recovery)

## Conclusion and Future Work
- Key takeaways for security practitioners
- Limitations of this research
- Next steps: Neural network target, black-box attacks, more defense methods

## Call to Action
- GitHub link
- LinkedIn connection
- Questions welcome
