# Importing Necessary Modules

from chatbot import Chat, register_call
import wikipedia

#Chat and register_call are classes/methods from the chatbot module.
wikipedia is imported for querying information from Wikipedia.

# Registering a Custom Call:

@register_call("customWhoIs")
def who_is(session, query):
    try:
        return wikipedia.summary(query)
    except Exception:
        for new_query in wikipedia.search(query):
            try:
                return wikipedia.summary(new_query)
            except Exception:
                pass
    return "I don't know about " + query
@register_call("customWhoIs") decorates the who_is function, registering it with the name "customWhoIs."
This function uses Wikipedia to fetch a summary for a given query. If unsuccessful, it tries alternative queries.

#Disabling GUI for Non-Interactive Environment:

def converse_no_gui(self, first_question):
    response = self.respond(first_question)
    print(response)
    while True:
        user_input = input("> ")
        if user_input.lower() in ["exit", "quit", "bye"]:
            print("Thank you for talking with me.")
            break
        response = self.respond(user_input)
        print(response)
converse_no_gui is a custom method to enable conversation without a graphical user interface (GUI).
It prints the response for the initial question and enters a loop to interact with the user through the console.

# Monkey-Patching the converse Method:

Chat.converse = converse_no_gui
 Monkey-patching involves modifying or extending a module or class at runtime. Here, we replace the converse method of the Chat class with our custom method.

# Having a Conversation with the Chatbot:

first_question = "Hi, how are you?"
Chat().converse(first_question)
The conversation starts with an initial question ("Hi, how are you?") using the converse method.
In summary, this code sets up a simple chatbot using the chatbot module, registers a custom call for querying Wikipedia, and adapts the conversation for a non-interactive environment. The conversation is then started with an initial question.
