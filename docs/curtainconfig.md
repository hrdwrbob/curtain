Device setup:
* All hardware devices auto set to pro audio
* Hardware devices not exposed to PJ, PJ creates pipewire virtual devices only.
  * Arbitrary channels and names.
  * add source -> add channel [choose from hw/channels] -> select location [FR/FL,etc]
  * hardware list (by grouping because pro audio)-> button to 'add as PJ device'


PLumb Sink (optional Context: Pressing Basket -> selected Plumb Source)
 - standard actions:
  - solo (disconnect all other sinks from source)
  - mute (mute - if in context mute src-sink level control)
  - level (change level - if in context, insert a level control filter src-sink and adjust that)
  - sel (un/link src-sink toggle if in context)
  - rec (Cycle through filters and show controls?)
Plumb Source (optional Context: Plumb Sink) 


base controls (comes from what is being controlled):

Note controls are grouped, and ordered, so that they populate in the same way all the time.


levels 
 - inc/dec
 - preferred: fader, rotational
 - set
  - min/max
  - curve
   - linear
   - fit
    - pairs of values 
   - log
values
toggles
buttons


Pressing Baskets
 Baskets of controls
 A pressing basket can be active or inactive, but can also be overlaid over other controls (eg: for a filter). If a pressing basket is activated and any of the controls are already assigned, it becomes an 'overlay' pressing basket. You can request an in use pressing basket, which will create an overlay copy of that basket. When closed, this will revert back to previous controls. An overlay pressing basket will remove all previously assigned controls within it unless told otherwise. 
 eg: an overlay pressing basket for four Squish Baskets (channels) out of 8 in a Pressing Basket would not remove the Squish baskets 
Squish Baskets (can have context - points to another control basket OR can be hardcoded)
      

Squish Baskets (sub Pressing Baskets) - typically assigned to a channel or a filter, and controls assigned by hinting, or if hints not found, in order.
eg:
   level
   mute
   record
   select
   solo
   level2
   hint: context squish


Plumb Baskets
 Baskets of Plumbs
  - obviously.
 next
 prev
 nextpage
 prevpage

has a selected plumb
