# Workshop 7: Express routes
### Welcome to your 7th workshop!
In this workshop we will practice some javascript and also using express to build routes
We already have 3 routes implemented:
Root get route:
```javascript
app.get('/', (req, res) => {
    res.status(200).json({
        health: 'ok'
    });
});
```
Creating Jedi:
```javascript
app.post("/jedi", async (req, res) => {
    await jediService.addJedi(req.body);
    res.status(200).json(req.body);
});
```

Getting Jedi:
```javascript
app.get("/jedi/:id", async (req, res) => {
    let jediId = Number.parseInt(req.params.id);
    if (isNaN(jediId)) return res.status(400).json({
        status: 400,
        error: "wrong parameters"
    });

    const jedi = await jediService.getJedi(jediId);

    if (!jedi) return res.status(404).json({
        status: 404,
        error: "Not found"
    });

    res.status(200).json(jedi);
});
```
Your task is to create 3 additional routes:

1. ``PUT /jedi/:id``
which update jedi by given id with received body.
For that you need to implement corresponded method in ``jediService.replaceJedi(id, jedi)``
2. ``GET /jedi/``
which return list of all Jedi's. For that you will need to implement ``jediService.getAll()`` method
3. ``DELETE /jedi/:id`` which delete specific jedi. Corresponded method is ``jediService.deleteJedi(id)``

### Bonus:
4. ``PUT /jedi/dark_side`` finds Anakin Skywalker and turn him into Darth Vader
5. ``DELETE /jedi/:id/undo`` undo delete of previously deleted jedi