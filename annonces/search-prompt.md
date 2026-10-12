Run the Annonces Montpellier search now (on demand, same as the daily run).

The app lives at https://ghisfit.github.io/annonces/ and reads annonces/data.json in the repository ghisfit/ghisfit.github.io. It lists apartments for sale in Montpellier, up to 120,000 euros, for a student rental. The page cannot search by itself: you search and write the results into annonces/data.json.

0. Use the repository ghisfit/ghisfit.github.io (call add_repo with access "push" if it is not already attached, then clone it). Edit annonces/data.json only. Never touch any other file.

1. Read annonces/data.json. It is {"settings": {...}, "listings": [ {id, ...fields}, ... ]}.

2. Search: WebFetch https://www.pap.fr/annonce/vente-appartements-montpellier-34-g43621-jusqu-a-120000-euros and ask for every apartment listing with price, surface, rooms, neighbourhood and full URL. Keep only listings in Montpellier itself. Never invent a listing or a figure.

3. For each listing not already stored (id "pap-<reference number from the URL>"), WebFetch the listing page and add an object to "listings" with, in French: id, title, quartier, city, price (number), surface (number), rooms (number), floor, chargesYear (omit if not stated), taxeFonciereYear (omit if not stated), rent and rentNote (ONLY if the ad states an actual current rent), dpe (omit if not stated), transit, parking, students (faculties mentioned, or "Aucune faculté mentionnée dans l'annonce."), extras, note, url, source "PAP", status "new", seenAt (YYYY-MM-DD), addedAt (today, YYYY-MM-DD, never change it later), lat and lng (approximate centre of the neighbourhood or named tram stop; omit if unknown). On PAP, "À partir de X € / mois" is a loan estimate, NOT rent.

4. Stored listings no longer in the search: fetch the URL to confirm. If gone, prefix the note with "Annonce retirée le <date>." and set status "hidden". If a price changed, update it and mention the change in the note.

5. Set settings.updatedAt to today's date in French (e.g. "12 octobre 2026") and settings.lastRunDate to today (YYYY-MM-DD).

6. Check the JSON is valid (python3 -m json.tool), commit on main ("Annonces: refresh <date>") and push to main; if rejected, pull --rebase and push once more. The site updates about a minute later; tap "Actualiser" in the app to see it.

7. Reply in a few lines: new listings, removed ones, price changes, and the best new one for a student rental (near a faculty and a tram line). Facts from the ads only, no investment advice, no sellers' contact details. Write Japanese terms in English, never in Japanese script.
