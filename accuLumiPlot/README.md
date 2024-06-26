# scripts to make accumulated luminosity plots (works with newer CMSSW)

1. environment setup

```
scramv1 project CMSSW_13_0_10
cd CMSSW_13_0_10/src
git clone git@github.com:cms-DQM/DCTools.git 
cd DCTools/accuLumiPlot
bash
source setup_lumiplots.sh
```

2. Prepare the JSON file, the text file that contains the first and the last 
run numbers for the periods of interest (see point 5 if you want to make plots
only for the runs processed by DC), and find out the corresponding dates 
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

5. In order to produce accumulated luminosity plots for only the runs sent for DC, you have to prepare a full list of runs that are sent for central DC (not only the minimum and the maximum run numbers). Note, some of the runs are not sent for DC because of false siStrip or pixel DCS bits. If every partition of siStrip (TIBTID, TEC+, TEC-, TOB) and pixel (FPIX and BPIX) has false DCS bits, most likely they are turned off by the experts because we do not have stable beams (please double check) for the whole run. However, if only one or some partitions have false DCS bits, it is a real detector issue; although the runs are not sent for central DC, the runs must be included in the list of runs when making luminosity plots. 
```
python DCruns_create_public_lumi_plots_Run3.py runrange_public_brilcalc_plots_pp_2023_OfflineLumi.cfg
```
