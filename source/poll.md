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

