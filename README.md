# INDIGO DataCloud Tutorial: testing Ophidia for an astronomical image calibration task

Dear User,
in order to test Ophidia for the reduction of astronomical images you are kindly requested to follow
the procedure listed below. Before you start you should have already registered a new OphidiaLab
account and have received your credentials via email. If not, please register [here](https://ophidialab.cmcc.it/register/registration.html).

This tutorial presents the output of a use-case which is the result of a collaboration between
INAF (Trieste) and CMCC (Lecce) in the context of the INDIGO DataCloud European project for
the development and improvement of open-source cloud-based software.

**Ophidia** is a framework for data intensive analysis that exploits advanced parallel computing
techniques and smart data distribution methods. In particular, the point of strength that makes
it extremely efficient in parallel data processing is the adoption of an array-based storage model
and a hierarchical data organization for the distribution of scientific datasets over multiple nodes.
The framework was developed in the context of climate change and it has been mostly used in
that field up to now. With this use-case we aim at potentially extending its use to the field of
astronomy. Ophidia has been developed within the CMCC Foundation. More information about
the project can be found here: <http://ophidia.cmcc.it/>.

**OpidiaLab** is a science gateway that offers to the end-user the possibility to exploit the full
Ophidia potential directly from the browser. It includes a JupiterHub installation for the creation
and sharing of documents containing live code through the Jupiter Notebooks. Python bindings
are available for Ophidia (PyOphidia). OphidiaLab gives also the possibility to use the Ophidia
Terminal which is basically an Ophidia client with a functionality similar to that of the bash shell.
Both these features will be explored during the tutorial.

The image calibration test is based on a set of calibration images (bias and flats) and science
images that are already loaded into OphidiaLab. If you want to reduce your own set of images
please sent an email to londero@oats.inaf.it.

Thanks to an extension, developed in the context of this use-case, Ophidia can now read the
FITS format. The latest release of the software includes this feature. If you are interested to install
it locally on your machine, please download the code and follow the procedure described [here](http://ophidia.cmcc.it/the-official-release-of-ophidia-v1-1-0-is-available/).

Once loaded into Ophidia, two metadata keys are selected to identify the FITS files: the filter
type (FLT ID) and the observation type (OBS TYPE). For the set of images specifically used for
this tutorial, three different filters are found: B JOHN 10, V JOHN 11 and R JOHN 12. The
observation type specifies if an image is of bias, flat or science type. In case you want to reduce
your own set of images you must know the values of these two metadata keys in advance because
they need to be set in the Python script.

The tutorial begins here.

**Login to OphidiaLab**

1. By using the credentials received by email, login to OphidiaLab following the [link](https://ophidialab.cmcc.it/jupyter/hub/login).
2. Get acquainted with the environment: you can find a short guide explaining OphidiaLab
capabilities in your home folder under quickstart → Quick Start.ipynb
3. the folder INDIGO-FITS/fits-raw contains all the FITS files that are going to be used
for this calibration example

**The Ophidia Terminal**

1. Open an Ophidia Terminal by clicking on the New button on the top-right part of your
home page and select Terminal
2. use the command pdd to check your current directory;
3. use the command lsd to list directories and files;
4. load a FITS file giving the command:
    oph importfits src path=[path=/data/INDIGO-FITS/fits-raw;
    file=LRS.2016-06-06T20-30-03.925.fits];measure=mymeasure;
    exp dim=NAXIS1;imp dim=NAXIS2;container=FITS2
5. use ll to check that the cube has been loaded;
6. extract the metadata value corresponding to the FLT ID key:
    oph metadata mode=read;
    cube=https://ophidialab.cmcc.it/ophidia/236/61108;
    metadata key=FLT ID;metadata type=text;metadata value=test text;
7. delete the cube by issuing:
    oph delete cube=https://ophidialab.cmcc.it/ophidia/236/61107
8. if you want to learn more about the commands available from the Ophidia Terminal
you can check this page.

**Run the Python script**

1. download locally on your machine the script from [here](https://owncloud.ia2.inaf.it/index.php/s/xIpPHYeyXHJnniJ)
2. Click on the Upload button on the top-right part of your home page and search for the
file you want to upload
3. Click on the blue Upload button that it appears in your home; now you should see the
file among the Notebooks in your home
4. open it by clicking on it
5. in Section I fill in the credentials you used for accessing OphidiaLab; this way you will
connect to the server instance. Notice that from PyOphidia the modules client and
cube are imported: the first is used for submitting any type of request (from simple
tasks to workflows) while the second makes the direct interaction with the cubes (in
our case the metadata and data of the FITSfiles) possible. Click on the cell and run it
by using the run cell button
6. in Section II the FITS files are imported into Ophidia by specifying the path and the
dimensions of the file (NAXIS1 and NAXIS2 for optical images as in his case). Click
on the cell and run it. The following two cells set the value of the metadata for the
filters used and for the observation type (flat, science or bias). Run both the cells.
7. in Section III the median of all the bia files is calculated; run the cell.
8. Sections IV-VI: the median for the flat files is set-up without doing the calculation.
Each cell performs the operation for one particular filter. Run the cells.
9. Sections VII-IX: the median for the science images is set-up without doing the calcula-
tion. Each of the three cells performs the operation for a different filter. Run all the
cells.
10. Sections X and XI effectively calculate the median for the flat and science image re-
spectively. Run all the cells.
11. in Section XII the bias image obtained in Section III is subtracted from the three science
images resulting from Sections VII-IX. Run the cell.
12. in Section XIII the bias image obtained in Section III is subtracted from the three flat
images resulting from Sections IV-VI. Run the cell.
13. in Section XIV the three science images obtained in Section XII are divided by the flat
images obtained in Section XIII. Run the cell.
14. finally the result of the calibration procedure is written to a FITS file thanks to the
oph exportfits Ophidia operator. Run the cell.
15. now you can download the file and visualize it by using for example [fv](https://heasarc.gsfc.nasa.gov/ftools/fv/fv_download.html).

**Conclusions and final remarks**

This tutorial has shown how to use Ophidia for an astronomical image calibration task. In
order to make Ophidia competitive with other already available software and to extend its
use also to other astronomical analysis tasks, further development of the code is needed.
To this end it is important to us if you could express your degree of satisfaction with this
tutorial and we would also like to know your opinion on a possible future extension of the
Ophidia capabilities to the astronomical field. Would it be valuable for your research? The
survey you are asked to fill in can be found following this [link](https://form.jotformeu.com/72554203448354).
Thank you for your cooperation.
