# scripts to make accumulated luminosity plots (only works with older CMSSW, such as CMSSW_8_0_1)

Note, CMSSW_8_0_1 is only available at lxplus7 machines.

1. environment setup

```
scramv1 project CMSSW_8_0_1
cd CMSSW_8_0_1/src
git clone -b Legacy_CMSSW_8_0_1 git@github.com:cms-DQM/DCTools.git 
cd DCTools/accuLumiPlot
bash
source setup_lumiplots.sh
```

2. Prepare the JSON file, the text file that contains the first and the last 
run numbers for the periods of interest, and find out the corresponding dates 
of the first and the last runs (via OMS or run registry) and modify the input 
cfg file (using runrange_public_brilcalc_plots_pp_2023_OfflineLumi.cfg as your 
template). If a normtag_json is provided in the cfg, you are showing offline 
luminosity. Otherwise, you are showing the results of online luminosity. 
Please modify ```cache_dir```,```file_suffix```, and ```plot_label``` 
accordingly.


3. Run the script, take 2023 pp runs for example
```
python runrange_create_public_lumi_plots_Run3.py runrange_public_brilcalc_plots_pp_2023_OfflineLumi.cfg
```

4. In the example of 2023 and with a normtag_json, the figure to check is 
```
rr_int_lumi_per_day_cumulative_pp_2023OfflineLumi.png 
```
But note the file name may vary depending on the parameters given in the cfg 
file.

