Idea: Go from both sides, combine Path Tracing and Light Tracing.
#TODO: Overview from slide 25
## Key Observations
- Every path with $k$ vertices can be constructed using $k+1$ strategies
- For a particular path length, all strategies estimate the same integral, however:
- Each strategy has a different PDF, different strengths and weaknesses
	- Best to combine strategies with MIS
	- Doesn't make any sense without MIS, see Veach's MIS overview ([[CG 07V2 Global Illumination III]] Slide 29)
MIS idea: How probable is this path with this strategy vs across all other strategies? Strategies are weighed.
