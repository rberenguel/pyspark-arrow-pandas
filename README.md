# Internals of Speeding Up Pyspark with Arrow

Presentation I ([@berenguel](https://twitter.com/berenguel)) gave at the [PyBCN
meetup](https://www.meetup.com/python-185/) on June 2018, [Spark
London](https://www.meetup.com/Spark-London/) on September 2018, [Spark
Barcelona](https://www.meetup.com/Spark-Barcelona/) and [Spark Summit Europe
2019](https://databricks.com/session_eu19/internals-of-speeding-up-pyspark-with-arrow)
to explain how Spark 2.3/2.4 has optimised UDFs for Pandas use as well as how
PySpark works. A recording of this talk (the one given in Python Barcelona, in
English) is available [here](https://www.youtube.com/watch?v=698441URsrc), the
recording from Spark Summit should be available soon. You can find the slides
[here](https://github.com/rberenguel/pyspark-arrow-pandas/raw/master/pyspark.pdf)
(some images might look slightly blurry). I recommend you check the version with
[presenter
notes](https://github.com/rberenguel/pyspark-arrow-pandas/raw/master/pyspark-with-notes.pdf)
which is only available here.

If you want additional information about Spark in general, I gave an
introduction to Spark talk with [Carlos Peña](http://twitter.com/crafty_coder)
that you can find [here](https://github.com/rberenguel/WelcomeToApacheSpark).

---

This presentation is formatted in Markdown and prepared to be used with
[Deckset](https://www.decksetapp.com/). The drawings were done on an iPad Pro
using [Procreate](https://procreate.art). **Here only the final PDF and the
source Markdown are available**. Sadly the animated gifs are just static images
in the PDF.

---

You can find an exported version using [reveal.js](http://revealjs.com) of the
version given at Spark Summit
[here](https://rberenguel.github.io/pyspark-arrow-pandas/pyspark.html#/). It is
not 100% faithful to the PDF/Deckset version but is close enough (and animated
gifs play). The export was generated with
[this](https://github.com/rberenguel/awkrdeck) and tweaked to add a footer.

---

<style>.bmc-button img{width: 35px !important;margin-bottom: 1px !important;box-shadow: none !important;border: none !important;vertical-align: middle !important;}.bmc-button{padding: 7px 5px 7px 10px !important;line-height: 35px !important;height:51px !important;min-width:217px !important;text-decoration: none !important;display:inline-flex !important;color:#ffffff !important;background-color:#79D6B5 !important;border-radius: 5px !important;border: 1px solid transparent !important;padding: 7px 5px 7px 10px !important;font-size: 28px !important;letter-spacing:0.6px !important;box-shadow: 0px 1px 2px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;margin: 0 auto !important;font-family:'Cookie', cursive !important;-webkit-box-sizing: border-box !important;box-sizing: border-box !important;-o-transition: 0.3s all linear !important;-webkit-transition: 0.3s all linear !important;-moz-transition: 0.3s all linear !important;-ms-transition: 0.3s all linear !important;transition: 0.3s all linear !important;}.bmc-button:hover, .bmc-button:active, .bmc-button:focus {-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;text-decoration: none !important;box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;opacity: 0.85 !important;color:#ffffff !important;}</style><link href="https://fonts.googleapis.com/css?family=Cookie" rel="stylesheet"><a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/rberenguel"><img src="https://cdn.buymeacoffee.com/buttons/bmc-new-btn-logo.svg" alt="Buy me a coffee"><span style="margin-left:15px;font-size:28px !important;">Buy me a coffee</span></a>

---

![](https://raw.githubusercontent.com/rberenguel/pyspark-arrow-pandas/master/Images/PresentingSAIS.jpg)

![](https://raw.githubusercontent.com/rberenguel/pyspark-arrow-pandas/master/Images/Presenting.jpg)


