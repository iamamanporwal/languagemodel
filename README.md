## Problem Statement

1. Our app needs a Language model that can understand and summarize a person's personality, based on some multiple choice questions they answer about themselves.

## My approach for this solution

To solve these challenges, we can use OpenAI's API or other Open-source large language model. Here's why it's a good idea:

1. Building our own tool from scratch would take a lot of time and resources. Plus, the output could end up repetitive and robotic

2. We can train this API to work just the way we want it to for our app. Plus, it's easy to use with JavaScript, we'll not have any compatiblity issues.

## Here's a sample code of how it works (Python)
```
import openai

# OpenAI API key
api_key = 'key'

# User's responses to personality questions
user_responses = [
    "You value privacy and independence and prefer working alone or in small groups. You have a strong curiosity and desire for knowledge, which you pursue through observation. You may be introverted, preferring to observe and analyze situations from far away rather than be the center of attention. You are a strategic thinker, constantly evaluating scenarios and weighing potential outcomes. You wish for an invisibility cloak, which may suggest mistrust or suspicion towards others. However, it's not necessarily a negative trait; some people use it for self-defense based on their past experiences."
    # Add more user responses here
]

# Combine user responses into a single string
user_input = "\n".join(user_responses)

# Generate a personality summary using OpenAI API
openai.api_key = api_key
response = openai.Completion.create(
    engine="text-davinci-002",
    prompt=f"Generate a 1-2 line summary of this person's personality:\n{user_input}\n",
    max_tokens=50,  # Adjust the max_tokens for desired output length
    temperature=0.7,  # Adjust temperature for creativity
)

# Extract and print the generated summary
personality_summary = response.choices[0].text.strip()
print(personality_summary)

```
OUTPUT (3rd Person perspective)
```
This person is a reserved and inquisitive individual who thrives in solitude, possesses a strategic mindset, and may have a cautious nature shaped by past experiences.
```
OUTPUT (2nd Person perspective)
```
You prioritize privacy and independence, often choosing solitary or small group work. Your curiosity drives you to observe and analyze, and your desire for an invisibility cloak suggests a cautious nature shaped by past experiences.
```

## Additionally 
We can use this 3rd-person perspective output generated by the model to compute the similarity percentage between the personalities of two distinct individuals using TF-IDF from scikit-learn. This approach can also prove valuable for enhancing recommendation systems.
```
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
```

