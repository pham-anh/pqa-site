---
title: SRE
menu:
  notes:
    name: SRE
    identifier: notes-sre
    weight: 150
---

{{< note title="SRE key notes" >}}

# SRE key notes

- Change is best when small and frequent.
- Design thinking methodology has five phases: empathize, define, ideate, prototype, and test.
- Failures need to be fast (unless we will spend too much time for nothing)
- Resistance to change is usually a fear of loss.

- **Blameless postmortem**: Detailed documentation of an incident or outage, its root cause, its impact, actions taken to resolve it, and follow-up actions to prevent its recurrence.
- **Reliability**: The number of “good” interactions divided by the number of total interactions. This leaves you with a numerical fraction of real users who experience a service that is available and working.
- **Error budget**: The amount of unreliability you are willing to tolerate.
- **Service level indicator (SLI)**: A quantifiable measure of the reliability of your service from your users' perspective.
- **Service level objective (SLO)**: Sets the target for an SLI over a period of time.

Bias

- **Selective attention bias**: Tendency to pay attention to things, ideas, and input from people whom you tend to gravitate toward. (Xu hướng chú ý có chọn lọc)
- **Affinity bias**: Tendency to gravitate toward those who are similar to you, such as with race, gender, socioeconomic background, or education level.
- **Labeling bias**: Tendency to form opinions based on how people look, dress, or appear externally
- **Confirmation bias**: Tendency to find information, input, or data that supports your preconceived notions.

SLI correlates with users' experience with the service

Measure toil

Monitoring

Organizations with high SRE maturity have well-documented and user-centric SLOs, error budgets, blameless postmortem culture, and a low tolerance for toil.

Links

- [https://dora.dev/quickcheck](https://dora.dev/quickcheck)


{{< /note >}}