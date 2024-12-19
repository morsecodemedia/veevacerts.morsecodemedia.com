# https://veevacerts.morsecodemedia.com/
A tool for studying for Veeva certifications.

Live text search on questions.

## Contributing
More Coming Soon...

### Question/Answer JSON Object
The JSON object is saved in the `static` folder as `master.json`.

Use the following format for the questions and answers. You are able to have as many answer options as needed for each question. This also allows you to select multiple correct answers.
```
{
    "certificationName": [
        {
            "question": "Question Placeholder",
            "answers": [
                {
                    "option": "Answer Placeholder 1",
                    "valid": "Correct"
                },
                {
                    "option": Answer Placeholder 2",
                    "valid": "Incorrect"
                }
            ]
        }
    ]
}
```