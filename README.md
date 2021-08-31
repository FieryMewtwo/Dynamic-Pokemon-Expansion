# Dynamic-Pokemon-Expansion [FR]

## What is this:
A dynamic data insertion tool for expanding Pokemon data in FireRed.

## Features:
* Dynamic insertion, meaning no worrying about repointing ever!
* Support for as many different Pokemon (regular Pokemon, forms, etc.) as you'd like.
* Support for different gendered forms.
* Support for different form Pokedex entries like in Sun/Moon.
* Support for up to 999 different Pokedex entries (not including alternate forms).
* Support for FRLG habitats.
* Support for Pokemon sprite and icon insertion.
* Support for cry insertion.
* Support for up to 128 TM/HM's and 128 Move Tutors

**NOTE** It is highly recommended to apply the [Complete Fire Red Upgrade](https://github.com/Skeli789/Complete-Fire-Red-Upgrade) following the insertion of this hack. Otherwise, make sure to comment out the  line ``#define EXPAND_LEARNSETS`` in the defines file or your game will crash (unless you have expanded movesets manually).  Additionally, if you're **not** using the Complete Fire Red Upgrade, in [bytereplacement](https://github.com/Skeli789/Dynamic-Pokemon-Expansion/blob/master/bytereplacement), find the changes for the seen  and caught flag ram, and change it to some free  save space. Make sure to apply a saveblock hack first and a TM/Tutor expansion first, though.

## Installation Instructions:
See the [Wiki](https://github.com/FieryMewtwo/Dynamic-Pokemon-Expansion/wiki)

## About TM/HM & Move Tutors
When looking in the ``src`` directory, you will notice two subdirectories, ``tm_compatibility`` (for modifying TM/HM data) and ``tutor_compatibility`` (for modifying Move Tutor data). Contained within these directories are files corresponding to each TM/HM and Move Tutor. Unlike most tools and expansions, this engine allows modification by TM/HM and Move Tutor number, as opposed to by species. To give a species a certain TM/HM or Move Tutor, simply add the species name to the appropriate file. If you want to change one of the pre-defined TM/HM's or Move Tutors, simply change the name of the file (leaving the number the same), and update the corresponding data in the files ``include/tutors.h`` and/or ``src/TM_Tutor_Tables.c``.

## Extracting Old Data:
When using this expansion, you may wish to keep using the sprites already inserted in your rom. If so you will need to extract the original graphics data pointers from your rom. To do this, overwrite the ``BRPE0.gba`` file in the root with this rom that has the graphics data (always make a backup first!). Then, open [scripts/data_extractor.py](https://github.com/Skeli789/Dynamic-Pokemon-Expansion/blob/master/scripts/data_extractor.py) and change the line ``NumberOfPokemon`` to the number of species graphics data you wish to extract from your rom + 1. Go back to the root, open the command line, and type ``python scripts//data_extractor.py``. Extracted graphics data will be pulled from your rom and placed in a new folder ``extracted``. Copy the contents of the **tables** found in these files and overwrite the **tables** found in the equivalent files found in [src](https://github.com/Skeli789/Dynamic-Pokemon-Expansion/tree/master/src). Once the extraction is complete, make sure to either add ``(void*)`` to the beginning of each pointer in these extracted files, or open ``include/graphics.h`` and replace any relevant instances of ``const u8*`` with ``u32``. This will allow the files to compile warning free. Now, the next time you insert this hack, all of your graphics pointers will remain unchanged, allowing you to make changes to things such as the Pokedex data and level-up movesets without worrying about repointing anything.
