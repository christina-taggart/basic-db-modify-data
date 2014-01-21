Release 0:

Texas Senators:
Sen. Kay Hutchis
Sen. John Cornyn

1.
INSERT INTO voters(first_name, last_name, gender, party, party_duration, age, married, children_count, homeowner, employed, created_at, updated_at)
   ...> VALUES('Spencer', 'Smitherman', 'Male', 'Republican', 10, 23, 0, 0, 2, 1, 'now','now');
INSERT INTO voters(first_name, last_name, gender, party, party_duration, age, married, children_count, homeowner, employed, created_at, updated_at)
   ...> VALUES('Holly', 'Hayes', 'Female', 'Democrat', 10, 23, 0, 0, 2, 1, 'now','now');

2.
INSERT INTO congress_members(name, party, location, grade_1996, grade_current, years_in_congress)
   ...> VALUES('Donald Trump', 'Republican', 'NJ', 10, 9, 1);
New Jersey Senators:
Sen. Frank Lautenberg (NO MORE!)
Sen. Robert Menendez

UPDATE congress_members
   ...> SET name='Sen. Donald Trump', party='Republican'
   ...> WHERE id=102;

DELETE
   ...> FROM congress_members
   ...> WHERE id = 531;

Release 1:

1.
DELETE
   ...> FROM voters
   ...> WHERE voters.id IN
   ...> (SELECT voters.id FROM voters
   ...> JOIN votes ON voters.id = voter_id
   ...> WHERE party NOT IN ('Republican','Democrat')
   ...> GROUP BY voters.id
   ...> HAVING COUNT(voter_id) < 2);

2.
DELETE
   ...> FROM voters
   ...> WHERE homeowner = 1 AND employed = 1 AND children_count = 0 AND party_duration <3 AND id IN
   ...> (SELECT voter_id FROM votes
   ...> WHERE politician_id IN (SELECT id FROM congress_members
   ...> WHERE grade_current > 12));

   Release 2:

1.
UPDATE votes
   ...> SET politician_id = 346
   ...> WHERE voter_id IN (SELECT id FROM voters
   ...> WHERE age > 80 and children_count = 0);
2.
UPDATE votes
   ...> SET politician_id
   ...> = (SELECT id FROM congress_members
   ...> ORDER BY grade_1996 LIMIT 1)
   ...> WHERE politician_id=(SELECT id FROM congress_members ORDER BY grade_1996 DESC limit 1);