# Methods in Life Science

> Freie Universität Berlin.

## Getting Started

### Setup

 - Data:

The data is under the [assets](/assets) folder.


exons_df = exons_df.sort_values(by=['Gene', 'mRNA', 'Start'])
exons_df['Start_Below'] = exons_df.groupby('mRNA')['Start'].shift(-1)
intron_df = exons_df[['SeqID', 'Gene', 'mRNA', 'End', 'Start_Below', 'Strand']]
intron_df = intron_df.dropna()
intron_df['End'] += 1
intron_df['Start_Below'] -= 1
intron_df = intron_df.rename(columns={"End": "Start", "Start_Below": "End"})

#size column
intron_df['Size'] = intron_df['End']-intron_df['Start'] + 1

#some adjustments
intron_df = intron_df.astype({'End':'int', 'Size':'int'})
intron_df = intron_df.reset_index(drop=True)
intron_df
