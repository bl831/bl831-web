---
title: S-SAD Data Collection
layout: default
group: data_collection
---

<nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="/procedures/data_collection/data-collection/">Data Collection</a></li>
    <li class="breadcrumb-item active" aria-current="page">{{ page.title }}</li>
  </ol>
</nav>

---

# S-SAD Notes by James Holton

---

2014:  
                        James Holtons's S-SAD data collection recommendations to user:
____________________________________________________________________________________

I recommend very short exposures first (about 1 s or less in most cases) for 360 degrees in "inverse beam" 

(program in 180, and tick the "inverse beam" check box), then do the same thing at 4x the exposure, then 16x, 

etc.  Until the crystal is dead.  Best to do all this at 7235 eV because the detector calibration for S-SAD is 

best there.  Adjust the detector distance appropriately.

>>> A couple questions from the user:

 1) Could you define what you mean by "until the crystal is dead"?  If we started off at 1 sec and collected 360 

frames, then ran another collection at 4 sec, I would expect to be losing high resolution spots.  Is this where 

you would cut it off?  Or do you mean when even the low res spots are fading out?  Since you said to then do 16 

sec, etc. I am wondering if you mean to keep going until there are no spots left on the detector (or no spots 

beyond say 10 ?).

 2) Sounds like we should skip the fluorescence scan and just go straight to 7235 eV.  What about a remote 

energy for 2 wavelength MAD?  Or do you think sticking with a single wavelength is best?


>>>> Holton's reply:

What I mean by "dead" is about 30 MGy for most crystals (3e7 J/kg of absorbed x-ray energy), or ~30-60 minutes 

of shutter-open time for a typical crystal in the x-ray beam at 8.3.1.  The idea is that if mergeing all the 

data doesn't work, you can start cutting off the more "burnt" stuff to systematically see if things improve.  

The optimal "starting" exposure is generally the shortest exposure you think you can do and still index and 

process the dataset.  For most crystals 1 second is more than enough.  In your case it might be quite a bit 

shorter.  But don't go below 0.1 second because beam flicker starts to become a source of error when you do 

that.

Yes, there is no point trying to do a fluorescence scan with S-SAD because the sulfur edge (2.5 keV) is far too 

soft to be practical in a beamline that is full of air.  That is, 2.5 keV photons are almost completely absorbed 

in the air before they reach the crystal, let alone the detector.

For the same reason, there is no point trying to do "MAD", because you can't get anywhere near the S edge for 

the inter-wavelength differences to be useful. The absorption effects are too strong.

The 7235 eV recommendation comes from the way the detector is calibrated.  This seems to be the optimum place to 

collect anomalous from inaccessible edges (like S, Iodine, Xenon, etc). What you want for weak signals like this 

is a LOT of multiplicity.  Don't worry so much about resolution for getting phases, you never phase the outer 

half of your data anyway.  For that, you do refinement, and you can refine against a dataset collected 

explicitly for the high-res data.  The optimum exposure time for a native dataset is one where the background 

around your highest-angle spots is about "100" on the ADXV screen.  This is the point where detector read-out 

error is completely buried in the background, and longer exposures are just equivalent to the sum of shorter 

exposures, so you might as well divide and conquer.
____________________________________________________________________________________

  >>>>>  THESE recommendations have evolved over the years
  >>>>>   In chronological order, here are some earlier email edits,
  >>>>>  which contain additional information.  Of particular interest would
  >>>>>  be determining minimum crystal size need and completeness of data
____________________________________________________________________________________
 
11/11/03
 
> Subject: Low energy limit
 
> > What is the low energy limit on 8.3.1??

 -->>> J. Holton reply:

>
> The main thing stopping low-energy light at 8.3.1
> is air.  Our peak flux is actually around 3-4 keV,
> but air knocks the maximum up to 11 keV.  Still,
> we have useful flux down to 6 keV, 5 is possible,
> but then you have to start worrying about Si(333)
> contamination.  Let me know if you want to go down
> that far, and I can show you how to do it.
>
 
> > How is flux at iron edge if you can get there??
>
> We get 1.1x10^11 photons/s at 7keV.  The
> absorption of protein here is 5x higher than at
> 12keV.  A rough calculation suggests you can
> expect your crystals to last 3-4 hours.
>
> Hope this is helpful!
>
> -James
>
 
*****************************************************************************************************
 
6/15/05
 
> Hi James,
> We are trying to figure the best approach for the situation I'll describe
> below.  We thought we'd see if you had any advice or ideas.
>
> The situation is that we have collected three data sets from three
> crystals each to about 2.5A resolution.  The data look good so far.
> Unfortunately, I haven't been able to reproduce these crystals so all
> we have are native crystals.  We are think this is because of some
> degradation occurred that allowed the crystal formation.  We're working
> on figuring this all out and maybe making new constructs.  In the mean
> time we're in a bit of a race with another group to solve this
> structure.  We have about a dozen more crystals in the drops.  We need
> to collect data to phase these things.  Our thoughts were to try the
> standard soaks of heavy metals but we don't want to waste to many of
> our remaining crystals trying things out.  We also thought about
> bromide and iodide soaks.  Finally we thought about sulfur SAD.
> Incidentally elves, thought the space group was P222 or P22121.
>
> We have little no experience with the halide and sulfur methods and we
> were wondering if you have such experience or know if people have tried
> this on 8.3.1.
> Also, do you think these are worth while to try out or not?
>
> Anyway, any thoughts, pointers, ideas, on the matter would be much
> appreciated.
> Thanks

 -->>> J. Holton reply:>
 
First thing you want to do is look at your I/sigma ratios for the datasets
you've got so far.  If you're doing MAD or SAD then you're going to need:
 
I/sigma > 1.3*sqrt(kDa/sites)/f"
 
This "threshold" is where the signal-to-noise ratio of the anomalous
differences becomes one.  Surprizingly, you can solve MAD/SAD structures
even with a signal-to-noise rato that is that bad, but you can't go much
lower than that.  The unfortunate thing about this, however, is that when
DANO/SIGNADO ~ 1 there is no way to tell IF you have an anomalous signal at
all.
 
If you plug S SAD into this equation you can probably see why it almost
never works.
 
Then there's the "damage limit".  Native crystals don't absorb as much
energy as heavy-atom soaked ones, and the concentration of heavy atom can
very strongly effect crystal lifetime.  Unfortunately, there are no good
data on what you can and can't get away with.  Empirically, for the
crystals I am using to study this, you seem to always be safe with < 300s
or so of exposure in 8.3.1.  you might be able to get away with as much as
1000 or even 3000s in favorable cases.  I am developing a procedure to try
and preemtively measure how much energy a crystal is absorbing and figure
that into a data colleciton strategy, but I havn't got this working yet.
Rule of thumb is 300s.
 
You will probably be left with the situation where 300s will not give you
the I/sigma you need.  This is why solving structures is so hard.
 
In general, I would recommend the philosophy of one crystal at a time, and
see how often you can get yourselves over here.  Each of your crystals will
last not more than ~1 hour in the full x-ray beam, so it shouldn't be hard
to figure out what your data collection time is going to be.  (Note,
reducing the divergence will proportionally increase the expected sample
lifetime).
 
We have had one success (Clare Peters-Libeu) using Pt for RIPAS phasing,
where you use an intentionally damaged dataset as a "native" for phasing.
Others around the world have reported a few sucesses with RIPAS using
Iodine.  It's a strong signal when it works, but you need to have the
situation where your heavy metal decays a lot faster than anything else.
Otherwise, non-isomorphism kills you.  Much like it does in MIR.
 
Anyway, I hope this is helpful in some way.  Let me know if you have any
more questions.
*****************************************************************************************************
 
 
2/5/07
 
 Hi James,
 I am going to your beamline for data collection next week.
 Could you please let me know the wavelength range of 8.3.1
 and whether it is possible to do a sulfur-SAD type experiment there?
 Thanks a lot and see you soon.
 
 -->>> J. Holton reply:
 
A graph of the photon flux at 8.3.1 vs photon energy is available here:
 
http://bl831.als.lbl.gov/~jamesh/831_flux_curve.gif
 
The green line is the time you can expect a crystal to survive in the beam for
each photon energy.  Depending on your crystal's elemental composition, this
can move up or down (heavier metals make crystals die faster).
 
The most success we have had with sulphur-SAD is at 7000 eV (~1.8A).  This
seems to be the best compromise between the systematic errors introduced by
sample absorption and the strength of the anomalous signal from sulphur.
 
You can calculate how much data you will need for a given S-SAD experiment:
 
I/sd >= 1/3*sqrt(mass/sites)/f"
where:
I/sd   - is the signal-to-noise ratio you need in your data set
mass - is the mass of the protein in Daltons
sites  - is the number of sulphur sites you expect for the above mass
f"      - is 0.7 for S at 7000 eV
 
For example:
lysozyme weighs 14,000 Da and has 10 S atoms in it, so you need I/sd > 67
which is not too difficult to acheive with lysozyme.  On the other hand, a 100
kDa protein with ~ S sites is not something I would recommend people try to
solve with S-SAD.
 
Hope this helps!
 
-James
 
*****************************************************************************************************
6/26/07
 
Hi James,
    We have beamtime on the beloved 8.3.1 this Friday. And for once we have an
interesting experiment, a novel protein. We'd like to try one or more of the
following: MAD, MIR, Sulfur SAD. We're still establishing what derivates we'll
have so except for the S-SAD those are unknowns. We haven't done a S-SAD
before and the protein is rather large. Do you know what the practical limits
are for such an experiment? The protein is about 164kDa with 33 CYS and 46
MET, about 5.5% of the sequence. Is there a Xenon setup  available and is
8.3.1 amenable to that experiment? The crystals are quite robust. So far no
sign of resolution loss after 60 minutes on 7-1 at SSRL.
 
Naturally we need help in the set up for all the above.
 
Thanks in advance,
 
 -->>> J. Holton reply:
 
For MAD,MIR(AS) I recommend two wavelengths: halfway between the peak and
inflection and a high remote.  This gives the best compromise between signal
and damage.  8.3.1's new detector has very low read noise, so you should use
very very short exposures for MAD (1 second or less).  It is basically not
possible for read noise to corrupt anomalous differences, and radiation damage
rates are unpredictable.  Some heavy atom sites are very stable to
irradiation, but some (usually about half) decay very fast.  The "timescale"
of the fastest reactions is about 3-5 minutes in 8.3.1's beam.  So, keep your
first data set less than that.  After the first data set, re-do the
fluorescence scan.  In general, if there is a "white line" in the spectrum it
will fade if the heavy atom site is getting disordered.  If the white line is
still there, then take another data set with a longer exposure time.  Repeat
as necessary.  If the white line decays quickly, then you will need to use a
bunch of crystals and average the data to get enough signal.
 
In general, "enough signal" seems to follow this equation:
 
I/sd > 1.3*sqrt(MW/sites)/f"
 
where:
I/sd is the signal-to-noise ratio of the whole data set
1.3 is a bunch of constants
MW is the molecular weight in Da
sites is the number of sites in the above molecular weight
f" is the number of anomalous electrons in each site
 
So, for example, if you have a 164000 Da protein with 79 sulfur sites (f" ~
0.5 electrons at 7 keV), then you will need I/sd > 118 to solve the structure.
Since your average data set has I/sd ~ 22, and I/sd increases with the square
root of redundancy, you will need 29x the usual amount of data.  You will
probably not get this from one crystal.  60 minutes at SSRL 7-1 is roughly
equivalent to 2 minutes at ALS 8.3.1.
 
There is a Xe setup available, but it is in the upstairs lab.  George can help
you get access to it when you get here.  How much data you need depends on the
kind of site and the number of them.  If you have 10 Xe sites (9 e- at 7 keV),
then you only need I/sd > 18.5.  This is doable with one data set.  Similarly,
if you have SeMet, then you need I/sd > 15.5.
 
That's about all I can tell you with the information here.  I hope this can
guide your decisions sufficiently.  Sorry I won't be there.
 
Good luck.
 
-James
 
*****************************************************************************************************
 
8/18/10
   James,
 
  We're working on identifying novel ligands for our protein of interest,
 and we're particularly interested in a small molecule containing sulfur.
 Since the protein is relatively small (83 kD) and I've solved its structure
 to 1.45 A, we figured we could get phase information from
the anomalous scattering of sulfur, and at least find the
location of the non-Met sulfur (no Cys in protein).
It looks like this is done relatively often at synchrotron sources so if the
molecule is bound with high occupancy, we should be able to locate it.
I just wanted to ask an expert on some of the intricacies of performing
such an experiment at 8.3.1.
I've seen in the literature that groups have used sulfur SAD at wavelengths > 1.5 A,
that shouldn't be a problem at 8.3.1 right?
 Do you know of a "magical" wavelength for maximizing the sulfur scattering
or should I just try a few, assuming I bring a number of quality crystals?
    Thanks for your help,
 
 
 -->>> J. Holton reply:
 
The best "compromise" between air/sample absorption effects and the signal
from S is around 7 keV (1.77 A). I wouldn't go much lower than that.
 If you do, the errors from inaccurate absorption corrections start
to dominate the total error, and those don't "average out" as easily as random errors.
 
Still, using my calculator:
http://bl831.als.lbl.gov/xtalsize.html
 
You will have a Bijvoet ratio of 0.2% with 1 S in 83 kDa.
 The current standing world-record is a Bijvoet ratio of 0.5%.
 Your Bijvoet ratio will require a signal-to-noise ratio in the data of 750,
 which implies a needed multiplicity of 620-fold or more.
This is not impossible, but obviously challenging.
 
If you already have phases and all you want to do is SEE the S atom,
then you might be able to get away with less redundancy.
Essentially, you will only need anomalous data to low resolution,
and small differences between bright spots are easier to measure.
 
Anyway, that's the theory.  Good luck!
 
-James
 
*****************************************************************************************************
 
 Oct 4, 2011
 
> Hi James,
>
> I was wondering if you have had anyone trying to do sulfur SAD phasing at
> 8.3.1.  I've been trying to phase a structure with various heavy atom
> derivatives for a few weeks now without much success.  The protein is only
> 15kDa and has 7 sulfurs present (6 of which I believe are in disulfides).
> The crystals diffract reasonably well with a good crystal diffracting to
> about 2Å I'm going to be at 8.3.1 a couple times in the next few weeks (O/N
> shift tomorrow and a daytime shift next wednesday) and I'd be interested if
> you had any advice for how to go about collecting a sulphur SAD dataset.
>
>
> Cheers,
 
 -->>> J. Holton reply:
 
 
By my calculations:
http://bl831.als.lbl.gov/xtalsize.html
 
you'll need an average I/sigma(I) ~130 to do this. This is potentially do-able
with a multiplicity of 20 or more.
 
I recommend using 7200 eV as the photon energy. Always collect 360, and then
move the detector distance enough to put the spots on new pixels. Try to get a
few spheres per crystal. You may need to average DANO over several crystals to
get enough signal.
 
Let me know how it goes!
 
-James
 
*****************************************************************************************************


   $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

