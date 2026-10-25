# Rootly

Rootly helps people care for their own plants and discover other people's plants nearby.

## Language

**Plant**:
A single plant owned by a user, identified by a mandatory personal name. Its species is optional.
_Avoid_: specimen, greenery, houseplant, collection item

**Owner**:
The user who owns a Plant.
_Avoid_: parent, gardener, collector

**Profile**:
The public-facing identity of an Owner together with the Plants they choose to show.
_Avoid_: account, page, collection

**Username**:
The unique public identifier an Owner chooses for their Profile, displayed with `@` and used in the Profile URL.
_Avoid_: handle, screen name

**Display Name**:
The non-unique public name shown on a Profile.
_Avoid_: real name, nickname

**Coarse Area**:
The grid cell an Owner chooses for their Public Plants. It is not an address, neighborhood name, or exact coordinate.
_Avoid_: exact location, address, coordinates

**Public Plant**:
A Plant its Owner has chosen to show on their Profile and the Map.
_Avoid_: shared plant, listed plant

**Species**:
The kind of plant a Plant belongs to. A Plant may have no Species.
_Avoid_: type, variety, kind

**Catalog Species**:
A Species in Rootly's curated list, carrying care guidance.
_Avoid_: known species, supported species

**Custom Species**:
A free-text Species name entered by an Owner that is not in the catalog and carries no curated care guidance.
_Avoid_: other, unknown plant

**Archived Plant**:
A Plant its Owner has retired. It is hidden from the active list, reminders, and Map, but its history is retained.
_Avoid_: dead plant, deleted plant

**Care Action**:
A type of care tracked in v1: watering or fertilizing.
_Avoid_: task, chore

**Care Log**:
A record that an Owner completed a Care Action for a Plant at a time.
_Avoid_: watering event, check-in

**Care Schedule**:
The interval between Care Actions for a Plant.
_Avoid_: reminder, timer

**Reminder**:
The daily digest notification listing due Care Actions by Plant name.
_Avoid_: alert, push

**Care Card**:
The structured care guidance attached to a Catalog Species: light, watering, fertilizing, soil, temperature, toxicity, and a short note.
_Avoid_: article, guide

**Growth Entry**:
A dated record about a Plant containing at least one photo, Measurement, note, or Event.
_Avoid_: log, update, progress post

**Measurement**:
A numeric observation in a Growth Entry: height/length, width, or leaf count.
_Avoid_: metric, dimension

**Event**:
A categorized occurrence recorded in a Growth Entry, such as repotting, pruning, flowering, propagation, or pest/disease.
_Avoid_: milestone, activity
