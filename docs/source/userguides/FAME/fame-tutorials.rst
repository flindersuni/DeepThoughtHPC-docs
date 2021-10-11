===================================================
FAME: Bioinformatics Series
===================================================
----------------
Activate Python
----------------
We are going to use conda to install and update software. Before we begin, we need to activate the python module that is not initiated by default.

We are going to use vi again to add the python module activation so that we don’t need to do it every time. Copy this line and press Enter.

``vim ~/.bashrc``

Use the arrow keys to move to the line after the line that says module load slurm, and press i to switch to --INSERT-- mode.

Paste this text:

``module load python/3.9.6``

Press the Escape key, and then type :wq to save the changes and exit. (Note that here we combine the :w and :q commands!)

Now run this command to activate Python:

``source ~/.bashrc``

You should be able to type this command and get a response now:

``python3.9 --version``

------------------------
Download Conda  / Mamba 
------------------------

``From the HPC Team: No need to download conda - there is a module for you! module load Miniconda3 will get you up and running for conda. 
You can also follow these instruction if you would like you own copy of conda.``

Head to the miniconda download page and download the appropriate installer.

You want the one from Latest Miniconda Installer Links. Get:

    Linux Installer
    Python with the biggest number
    Miniconda3 Linux 64-bit

Here is a quick way to download that script!

Right click on the appropriate link, and choose Copy link address. Go back to your terminal window (probably Putty) and type wget and a space, and then paste the URL that you just copied. Press return and it should download the file for you!

The file should be called Miniconda3-latest-Linux-x86_64.sh but in case it is not, just substitute the appropriate file name below. Remember that you can check with ls -ltr to see the newest file downloaded.

Run the miniconda installer:

bash Miniconda3-latest-Linux-x86_64.sh

This will ask you some questions, and you can pretty much accept the default answer to all the questions.

Once the installer has finished the best way to continue is to log out, and then log back in. This will reset your account and you will have conda activated. At the bottom left of your screen you should see it say (base) which means that you are in the base conda installation.
Conda is great, but Mamba is better!Permalink

Mamba is a drop in replacement for conda, and it is the first thing we will install.

conda install -c conda-forge mamba

This will take a moment to set everything up and figure out what needs to be installed, and then ask you if you are sure.

Type yes and press return and mamba will be installed. From here on out, forget conda and think mamba!
Install your first bioinformatics packagePermalink

We are going to install prinseq++ and test to see if it works. This will demonstrate how to install a conda package. We make a new environment named bioinformatics and use the conda-forge and bioconda channels to install prinseq++

mamba install -c conda-forge -c bioconda prinseq-plus-plus 

Again, this will work on resolution of the packages for you and ask if you are sure. Once it is complete, you should be able to issue the command:

prinseq++ -v

to see the version of prinseq++ that has been installed.
Install snakemakePermalink

For the next steps of this tutorial, we are going to use snakemake to run some things on the cluster. So we are going to use mamba to install that:

mamba install -c conda-forge -c bioconda snakemake=5.22.0

    NOTE: At the time of writing, snakemake was introducing a new package called PuLP which makes the pipelining a lot faster, but is a bit glitchy. So we install version 5.22.0 which predates those changes. For more information see this issue, or this issue or this suggestion

Once that has completed, snakemake -v should show you the current version.
Install other bioinformatics packagesPermalink

You can install pretty much any bioinformatics package using conda. The anaconda website has a complete list and you can visit the bioconda page for more information about bioconda.

but to get started, you might want to install:

mamba install -c conda-forge -c bioconda blast focus diamond

Adding channelsPermalink

It is a pain to keep typing -c conda-forge -c bioconda so we can just add those two channels to our configuration

conda config --add channels conda-forge
conda config --add channels bioconda

Updating a packagePermalink

With conda (or mamba) you can easily update a package if there is a newer version. For example, to update snakemake you would use:

mamba update snakemake

What this means is the you are responsible for ensuring your software is up-to-date. Or not. If you are working on a set of data analyses you may want to keep all the software at the same version so that each time you do an analysis you get comparable answers. With conda, you have control over the update cycles, but don’t forget from time-to-time you might want to update the software!
EnvironmentsPermalink

If you want to keep different versions of software or run different pipelines you can do that with conda, in what are called environments. Each one can have different software. conda is clever, because if you have the same software in two different environments you don’t need an entire copy of the software. At this stage, you don’t need to worry about that, and you can just install everything in the base environment. But if you start to run into installation issues, then remember you can separate things into different environments.
Up nextPermalink