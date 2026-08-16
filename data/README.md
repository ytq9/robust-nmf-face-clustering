# Dataset layout

Place the downloaded ORL and Extended Yale B datasets in this directory before running the notebook. Dataset files are not committed to this repository.

Expected structure:

```text
data/
├── ORL/
│   ├── s1/
│   │   └── *.pgm
│   ├── s2/
│   │   └── *.pgm
│   └── ...
└── CroppedYaleB/
    ├── yaleB01/
    │   └── *.pgm
    ├── yaleB02/
    │   └── *.pgm
    └── ...
```

The loader ignores non-directory entries and Extended Yale B files ending in `Ambient.pgm`.

Use the official or institution-approved download source for each dataset and review its terms before redistribution.
