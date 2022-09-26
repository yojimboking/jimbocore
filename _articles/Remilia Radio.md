---
published: true
subtitle:
date: 2022-09-15
tags: projects lifestyle
---

# Remilia Radio

## Executive Summary

Remilia Radio is an algorithmic web radio platform emphasizing longform shuffle in segmented blocks to maximize both tonal coherency and variety from tightly curated libraries. Instead of the standard web radio of shuffled singles, RR is designed to play full length albums/EP's on shuffle, with music organized into genre segments replicating radio segments, with segments organized into time blocks intended to allow a natural tonal shift as the day progresses into night.

## Introduction

We launched with the Remilia Radio and YAYO Radio as two different takes on this concept, as an extension of our Lifestyle Design philosophy. Our intention is for radios can be left on to be played all day in the home, at the computer, or in the car. 

Developing your own radio is easy with a design that maximizes variety from curated libraries:

A Remilia Radio with 12 segments of 2 hours each only requires 60 albums per segment (or: 6 segments / 4 hours / 120 albums) to achieve a month's worth of unique, unrepeated music. You would require curating 14,600 singles (assuming ~3 minute single length) to achieve the equivalent variety in a traditional web radio of unsegmented shuffled singles.

Any enthusiast adept at deep dives can quite feasibly find 60-120 quality albums in any given niche genre or mood--it can often can be as trivial as identifying a well curated label.

## Motivations

### Why Album Shuffle

RR intends to correct past automated radio solutions. The standard software () attempts to mimic the traditional radio DJ's emphasis on singles. This works due to their hands-on curation; which may theoretically be replaced by algorithmic DJ'ing (e.g. stringing together adjacent keys & tags) in the future, but for now they rely on simple singles shuffling. 

Web radios end up forced to curate a very narrow single selection to ensure a basic coherency is followed from one song to the next song, usually defining the entire radio based on single, specific genres (e.g. "Deep House", "Ambient"). However, the need for a mass of singles to ensure a lack of repetition leads to lowering standards to include the most generic examples of the given genre. An examplary case study is SomaFM, one of the earliest internet radios.

These failings can be elegantly corrected by accepting the album record as the base unit of shuffling instead of the traditional radio single. Album releases are designed for home listening, intended for a sit-down experience, so they're already coherently ordered for a consistent and thoughtful mood throughout the ~1 hour length. 

This allows for a much wider net to be cast in every radio segment as you can be sure there are no harsh tonal or genre shifts within any given hour of an album. It also means the task of curating hundreds of hours of quality music is monumentally reduced.

### Why Segments and Blocks

A RR can be launched as a simple album shuffle of a single folder of content. However "genre" segments can be defined to allow a more versatile curation that shifts between different genres or moods without losing coherence within them, similar to a traditional radio moving between DJ's and their respective segments.

Segments also minimizes the collection size required to maintain variety.

### Why Time-Coded Blocks
Our radios are intended as utility radios, to left on playing all day at home or at the computer, or when out for a drive (or at the pool), and so we introduce natural tonal shift as each day progresses into night and morning again.

Segments can be randomly ordered, following the simple shuffle algorithm (Fisher-Yates), but we further introduce Time-coded Blocks to allow a higher-level of mood tied to the changing time of day, and exponentially increase the variety with same curated library size.

Multiple segments can be assigned to the same time-blocks as well as a segment included in multiple time-blocks.

## Settings

### Block Length

Blocks are 4 hours by default. Can also be set to any hour or minute length.

### Cut-off Albums

Default: Off

By default, albums will play to full completion even if it has gone over onto the next block. Turn this setting on will make the segment transition at the end of the current playing song.

### Prioritize MP3 Metadata
Default: Off

Block, Segment, Artist, Album Name and Track Title are pulled from the filename by default, and the mp3 metadata as a fallback. Turning this on will make the mp3 metadata take precedent.

### Fuzzy Transition

Default: On

By default, 15 minutes before a block is scheduled to begin, any new album will be pulled from the new block instead of the current one. Turn this off to wait only until end of hour. Setting is ignored if cut-off album is turned on.

### Allow Segment Repetition

Default: On

If a segment is assigned in multiple blocks, this setting will allow to be included in the random selection for the next block, effectively extending the segment's length. If off, then it will be ignored when picking the next block's segment.