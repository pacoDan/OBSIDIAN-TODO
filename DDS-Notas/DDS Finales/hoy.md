
**Contexto**
VideoTracker es una empresa que ofrece servicios de análisis del comportamiento de los usuarios al reproducir videos en línea. A través de un plugin integrado en los reproductores de video de los sitios que contratan el servicio, se recopila información en tiempo real sobre la interacción del espectador: en qué momento del video se encuentra, cuántas veces pausó la reproducción, cuántas veces cambió de pestaña, entre otros datos relevantes. Con esta información, se generan análisis detallados que permiten a los creadores de contenido y plataformas evaluar la recepción de sus videos, optimizar la producción y mejorar la experiencia de la audiencia.



Necesito estadísticas y análisis
El sistema ofrece estadísticas de 
los videos mas pausados
los videos que se dejaron de ver 
la tasa de porcentaje de los videos que si se vieron 
tasa de los videos que fueron minimizados

Además cada video posee tag por ejemplo, un video puede ser de tecnología, otro de documental, otro memes, otro video de noticias de la actualidad y mas tags

Además debes especificar las interfaces salientes y de entrada y ejemplos de json que se enviar y se reciben.

Ademas necesito tener guardado la trazabilidad de los intervalos de los videos que mas se reproducieron


todo esos analisis, metricas y observabilidad dame el diagrama de clases completa, recuerda que el usuario cliente usa el plugin en el navegador como medio de comunicacion hacia nosotros

el dashboard de analisis se muestra en el plugin



A su ves, el usuario podra brindar un feedback, de las metricas recibidas por el servicios externo que proceso los analisis generados



algunas clases teniendo encuenta elgunos pedidos de metricas:
+---------------------+
|      Video          |
+---------------------+
| - id: String        |
| - title: String     |
| - url: String       |
| - creatorId: String |
| - tags: List<Tag>   |
| - interactions: List<Interaction> |
| - statistics: Statistics |
+---------------------+
| + addInteraction(interaction: Interaction) |
| + getStatistics(): Statistics |
| + getTags(): List<Tag> |
| + getMostWatchedIntervals(): List<Interval> |
| + getTotalPauses(): int |
| + getTotalAbandonments(): int |
+---------------------+

+---------------------+
|     Interaction     |
+---------------------+
| - id: String        |
| - videoId: String   |
| - timestamp: long   |
| - type: InteractionType |
| - position: double   |
+---------------------+
| + getType(): InteractionType |
| + getPosition(): double |
+---------------------+

+---------------------+
|      Tag            |
+---------------------+
| - id: String        |
| - name: String      |
+---------------------+
| + getName(): String |
+---------------------+

+---------------------+
|   Statistics        |
+---------------------+
| - totalPlays: int   |
| - totalPauses: int  |
| - totalMinimizations: int |
| - totalViews: int   |
| - totalAbandonments: int |
| - viewRate: double   |
| - pauseRate: double  |
| - minimizationRate: double |
+---------------------+
| + calculateRates()   |
| + getTotalPlays(): int |
| + getTotalPauses(): int |
| + getTotalMinimizations(): int |
| + getTotalViews(): int |
| + getTotalAbandonments(): int |
+---------------------+

+---------------------+
|   VideoAnalytics     |
+---------------------+
| + analyzeVideo(video: Video) |
| + getMostPausedVideos(videos: List<Video>): List<Video> |
| + getAbandonedVideos(videos: List<Video>): List<Video> |
| + getMostWatchedIntervals(video: Video): List<Interval> |
+---------------------+

+---------------------+
|     Interval        |
+---------------------+
| - videoId: String   |
| - startTime: long   |
| - endTime: long     |
| - views: int        |
+---------------------+
| + getDuration(): long |
+---------------------+



--------------------------------------------------------------------------------------------------
+---------------------+
|      Metric         |
+---------------------+
| - id: String        |
| - name: String      |
| - description: String |
+---------------------+
| + calculate(): double |
| + getParameters(): List<Parameter> |
+---------------------+

+---------------------+
|   PauseMetric       |
+---------------------+
| - pauseThreshold: int |
+---------------------+
| + calculate(): double |
+---------------------+

+---------------------+
|   ShortVideoMetric   |
+---------------------+
| - durationThreshold: int |
+---------------------+
| + calculate(): double |
+---------------------+

+---------------------+
|   SkipMetric        |
+---------------------+
| - skipIntervals: List<Interval> |
+---------------------+
| + calculate(): double |
+---------------------+

+---------------------+
|     Parameter       |
+---------------------+
| - key: String       |
| - value: String     |
+---------------------+
| + getKey(): String  |
| + getValue(): String|
+---------------------+

+---------------------+
|   VideoAnalytics     |
+---------------------+
| + addMetric(metric: Metric) |
| + analyzeVideo(video: Video) |
| + getMetrics(): List<Metric> |
+---------------------+

+---------------------+
|      Video          |
+---------------------+
| - id: String        |
| - title: String     |
| - interactions: List<Interaction> |
| - metrics: List<Metric> |
+---------------------+
| + addInteraction(interaction: Interaction) |
| + getMetrics(): List<Metric> |
+---------------------+