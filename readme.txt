HAWAII RESERVES CASE STUDY

This repository contains data and configuration files used for a case study on obtaining reserves from load-shifting batteries and/or demand response, while transitioning to 100% renewable power in Hawaii. This file provides instructions for installing the Switch power system planning model, downloading the case study files, and running the case study.

INSTALL SWITCH MODEL

To run this case study, first install Switch version 2.0.0b4 or later. This version hasn't been merged into the master branch yet, so for now, this is the best way to do that:

1. Follow the installation instructions at https://github.com/switch-model/switch/blob/master/INSTALL.
2. At the command line, in the switch directory, execute these commands to use version 2.0.0b4:

git checkout 2.0.0b4

Note: It is highly recommended to use cplex, gurobi or equivalently fast solver for this case study. These can solve each case study in 5-10 minutes. glpk typically takes 10-100x longer.


INSTALL SWITCH-HAWAII DATA AND SWITCH MODEL CODE

After installing Switch, use the following commands to install and run the case studies.

Open a Terminal window or Anaconda command prompt. Then use the 'cd' and 'mkdir' commands to create and/or enter the  directory where you would like to store the case study data. Once you are in that directory, run the following commands (don't type the comments that start with '#'):

# download the SWITCH-Hawaii model and a matching version of the SWITCH model code
git clone --recursive https://github.com/switch-hawaii/reserve_study_2018.git

SETUP THE MODEL FOR YOUR FIRST RUN

You may need to edit main/options.txt to configure the model for your first run. The following should normally be changed before you get started:

-  Change the --solver flag and solver-related options to match the solver you are using (e.g., cplex or glpk); see notes in options.txt for advice on this.
- Change the --inputs-dir flag to choose the appropriate inputs directory; "inputs_tiny" is a small version recommended for testing; "inputs" is a medium size model which will usually solve within an hour; "inputs_12x24" is a larger model (12 days per period and 24 hours per day), which usually takes too long to solve when using the unit commitment and reserves modules.

RUN THE MODEL

You can solve the model at any time by launching a Terminal window or Anaconda prompt, cd'ing into the 'main' directory and then running this command:

switch solve-scenarios

You can add --help to see more options.

The "switch solve-scenarios" command solves all scenarios listed in scenarios.txt. This uses settings specified in options.txt, plus options specified in scenarios.txt, plus settings specified on the command line. Settings specified on the command line take precedence over those specified in the scenarios file, and both of those take precedence over options.txt. If your scenario definitions are stored in a different file (e.g., scenarios_ev.txt), you can specify that via the --scenario-list flag.

After the model runs, results will be written in tab-separated text files (with extension .tsv or .tab) in the "outputs_*" directories.

You can also inspect or change any of the model's input data by editing the *.tab files in the inputs* directories.
