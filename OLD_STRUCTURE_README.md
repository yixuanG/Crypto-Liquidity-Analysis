# Old Directory Structure - Safe to Archive

The following directories contain the original project structure and can be archived or removed after confirming the new structure works correctly:

## Directories to Archive/Remove

### 01_Dataset/
- Contains raw data files
- Already covered by .gitignore
- Can be moved to `data/raw/` if needed

### 02_batch_process_minute_e_spread/
- Old batch processing scripts
- **Replaced by:** `notebooks/02_data_conversion/`
- Contains outdated notebook versions (already deleted backups)

### 03_Event_Filter_&_Minute_Data_Panels/
- Combined old workflow
- **Replaced by:** 
  - `notebooks/01_event_filter/` (for event data)
  - `notebooks/03_event_hour_detection/` (for event hour detection)

### 04_Minute_Data_Preparation/
- Old data preparation scripts and outputs
- **Replaced by:** `notebooks/02_data_conversion/` and `notebooks/04_panel_generation/`
- Subfolders:
  - `5-year_minute_data_by_coins/` → Should go to `data/processed/`
  - `ms_to_min_conversion_code/` → **Replaced by** `notebooks/02_data_conversion/`
  - `panel_generator/` → **Replaced by** `notebooks/04_panel_generation/`

### 05_Impact_Intensity&Recovery_Analysis/
- Old analysis structure
- **Replaced by:** `notebooks/05_analysis/`
- Core notebooks already copied to new structure

### 06_data_prep_for_regression_analysis/
- Panel data for regression
- Should be in `data/processed/` or `results/panels/`
- **Replaced by:** Output from new panel generation notebooks

### 07_data_prep_for_spillover_analysis/
- Hourly panel data for spillover analysis
- Should be in `data/processed/` or `results/panels/`
- **Replaced by:** `notebooks/04_panel_generation/hourly_panel_generator.ipynb`

### Impact Model/
- Old model development folder
- Contains many duplicate and test versions
- **Replaced by:** Consolidated notebooks in new structure
- Subfolders contain ~1000+ files (mostly CSVs and PNGs)

### minute_data_prep/
- Duplicate of minute data preparation
- **Replaced by:** `notebooks/02_data_conversion/`

## Migration Checklist

Before deleting old directories:
- ✅ Core notebooks copied to `notebooks/`
- ✅ .gitignore created to exclude data files
- ✅ README documentation created
- ⚠️ Verify no unique analysis results are lost
- ⚠️ Check for any custom scripts not yet migrated

## Recommended Actions

1. **Keep temporarily:** Move old directories to an `_archive/` folder
2. **Test workflow:** Run through the new notebook structure
3. **Verify outputs:** Ensure analysis results are reproducible
4. **Final cleanup:** Delete archive folder once confident

## Safe Deletion Command

After verification, you can remove old directories:
```bash
# Move to archive first (safer)
mkdir _archive
mv 01_Dataset 02_batch_process_minute_e_spread 03_Event_Filter_&_Minute_Data_Panels \
   04_Minute_Data_Preparation 05_Impact_Intensity\&Recovery_Analysis \
   06_data_prep_for_regression_analysis 07_data_prep_for_spillover_analysis \
   "Impact Model" minute_data_prep _archive/

# Or remove directly (use with caution)
# rm -rf _archive/
```

---

**Created:** During project reorganization for GitHub publication
**Purpose:** Document old structure for reference before cleanup

