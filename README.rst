###########
Janna's fork
###########

Forked from https://git.ligo.org/lscsoft/ligo.skymap.git for the purpose of extending the plotting options for the ligo-skymap-plot tool.

The added options allow to modify the marker used in the --radec option (that marks a given RA DEC location). They are:

--marker MATPLOTLIB_MARKER
                        symbol used when marking --radec, has to be matplotlib
                        symbol (default: *)
  --marker-color MATPLOTLIB_COLOR
                        marker color used for --radec (default: white)
  --marker-ecolor MATPLOTLIB_COLOR
                        marker edge color used for --radec, has to be
                        matplotlib color string (default: black)
  --marker-size SIZE_INT
                        marker size used for --radec (default: 10)
                        
Additionally, I added options that are specifically useful when making skymaps for PTA (pulsar timing arrays). It marks the locations of pulsars from a text file. The file is assumed to have three columns: RA (deg.), DEC (deg.), RMS. The latter is the (average) noise level for the pulsar, which is used to scale the marker (bigger marker for lower noise pulsars). Pulsars are currently plotted as white stars with black outline (as is the default --radec marker), but the code could be edited to change this (see development notes below). The added options are:

  --mark-pulsars PATH_TO_PULSAR_FILE
                        markpulsars from file. Assuming columns ra, dec and
                        rms (noise level). (default: False)
  --max-pulsars INT     only plot first INT pulsars from mark-pulsars file
                        (default: False)


###########
Janna's install/development tips
###########

I installed ligo.skymap into a virtual environment from the repository, which allows developing the code to your own needs. Clone this repository or the original ligo.skymap one, then create a virtual environment and activate it::

   virtualenv my_venv
   source my_venv/bin/activate
   
Install the ligo.skymap requirements (note that I added astroquery to the requirements.txt because it wouldn't work for me without it). You have to be in the repository directory for this and the next step::

   python -m pip install -r requirements.txt
   
Install ligo.skymap itself with setup.py::

   python setup.py build install
   
Now you can run ligo-skymap-plot (or the other tools), with the additional marker options!
If you want to make further changes to ligo.skymap code, run the last command to install again. This builds the ligo-skymap-tool anew so it incorporates the changes.

...................Original ligo.skymap readme from here...............


###########
ligo.skymap
###########

The `ligo.skymap` package provides tools for reading, writing, generating, and
visualizing gravitational-wave probability maps from LIGO and Virgo. Some of
the key features of this package are:

*  `Command line tool bayestar-localize-coincs`_ and
   `bayestar-localize-lvalert`_: BAYESTAR, providing rapid, coherent, Bayesian,
   3D position reconstruction for compact binary coalescence events

*  `Command line tool ligo-skymap-from-samples`_: Create 3D sky maps from
   posterior sample chains using kernel density estimation

*  `Command line tool ligo-skymap-plot`_: An everyday tool for plotting
   HEALPix maps

*  `Module ligo.skymap.plot`_: Astronomical mapmaking tools for
   perfectionists and figure connoisseurs

To get started, see the `installation instructions`_ or the `full
documentation`_.

.. figure:: https://lscsoft.docs.ligo.org/ligo.skymap/_images/localization.svg
   :alt: GW170817 localization

   This illustration of the position of GW170817, prepared using `ligo.skymap`,
   illustrates the main features of this package: rapid localization of compact
   binaries with BAYESTAR [#BAYESTAR]_, three-dimensional density estimation
   [#GoingTheDistance]_ [#GoingTheDistanceSupplement]_, cross-matching with
   galaxy catalogs, and visualization of gravitational-wave sky maps.
   Reproduced from [#IlluminatingGravitationalWaves]_.

.. [#BAYESTAR]
   Singer, L. P., & Price, L. R. 2016, *Phys. Rev. D*, 93, 024013.
   https://doi.org/10.1103/PhysRevD.93.024013

.. [#GoingTheDistance]
   Singer, L. P., Chen, H.-Y., Holz, D. E., et al. 2016, *Astropys. J. Lett.*,
   829, L15. https://doi.org/10.3847/2041-8205/829/1/L15

.. [#GoingTheDistanceSupplement]
   Singer, L. P., Chen, H.-Y., Holz, D. E., et al. 2016, *Astropys. J. Supp.*,
   226, 10. https://doi.org/10.3847/0067-0049/226/1/10

.. [#IlluminatingGravitationalWaves]
   Kasliwal, M. M., Nakar, E., Singer, L. P. et al. 2019, *Science*, 358, 1559.
   https://10.1126/science.aap9455

.. _`Command line tool bayestar-localize-coincs`: https://lscsoft.docs.ligo.org/ligo.skymap/ligo/skymap/tool/bayestar_localize_coincs.html
.. _`bayestar-localize-lvalert`: https://lscsoft.docs.ligo.org/ligo.skymap/ligo/skymap/tool/bayestar_localize_lvalert.html
.. _`Command line tool ligo-skymap-from-samples`: https://lscsoft.docs.ligo.org/ligo.skymap/ligo/skymap/tool/ligo_skymap_from_samples.html
.. _`Command line tool ligo-skymap-plot`: https://lscsoft.docs.ligo.org/ligo.skymap/ligo/skymap/tool/ligo_skymap_plot.html
.. _`Module ligo.skymap.plot`: https://lscsoft.docs.ligo.org/ligo.skymap/#plotting-and-visualization-ligo-skymap-plot
.. _`installation instructions`: https://lscsoft.docs.ligo.org/ligo.skymap/quickstart/install.html
.. _`full documentation`: https://lscsoft.docs.ligo.org/ligo.skymap
