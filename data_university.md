#Day 1
##Kickoff
- Data engineer: uses data to build cool stuff.
- DE will use the Engineering background to create a reliable system (testable, monitored, HA)
- EndSong: what did you play, for how long, which user played the song
- important Pipelines: Pipeline Core (anonymous EndSong), ?
- Lesson learned: in Spotify a the question `is this something someone else should use?` ... what happened was that all the pipelines were available on HDFS so people started to be dependent between each other, it grew organically and now is pretty much a monster, see the PDF
- Is easy to build something, much harder to keep the owner
- TODO: [read Google Map/Reduce paper.](http://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf)
- `How does BigQuery plays here?` use BQ whenever is possible (simple SQL), use Scala when BQ cannot do it.

##Infra presentation
- Everyday we send reports to the media labels regarding the plays

##Second lecture: Scala

- immutability -> safer code
- Recursive functions require explicit definition of return type
- returns the value of the last expression
