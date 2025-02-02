# RAG
RAG documentation and code snipptes <br/>
Slide1: What is RAG<br/>
RAG stands for Retrieval Augmented Generation. It was introduced in the paper Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. <br/>
Each step can be roughly broken down to: <br/>
> Retrieval - Seeking relevant information from a source given a query. For example, getting relevant passages of Wikipedia text from a database given a question.
> Augmented - Using the relevant retrieved information to modify an input to a generative model (e.g. an LLM).
> Generation - Generating an output given an input. For example, in the case of an LLM, generating a passage of text given an input prompt. <br/>
Slide 2: Importance of RAG: <br/>
The main goal of RAG is to improve the generation outptus of LLMs. <br/>
Two primary improvements can be seen as: <br/>
1.	Preventing hallucinations - LLMs are incredible but they are prone to potential hallucination, as in, generating something that looks correct but isn't. RAG pipelines can help LLMs generate more factual outputs by providing them with factual (retrieved) inputs. And even if the generated answer from a RAG pipeline doesn't seem correct, because of retrieval, you also have access to the sources where it came from. <br/>
2.	Work with custom data - Many base LLMs are trained with internet-scale text data. This means they have a great ability to model language, however, they often lack specific knowledge. RAG systems can provide LLMs with domain-specific data such as medical information or company documentation and thus customized their outputs to suit specific use cases. <br/>
What kind of problems can RAG be used for? <br/>
RAG can help anywhere there is a specific set of information that an LLM may not have in its training data (e.g. anything not publicly accessible on the internet). <br/>
For example you could use RAG for: <br/>
•	Customer support Q&A chat - By treating your existing customer support documentation as a resource, when a customer asks a question, you could have a system retrieve relevant documentation snippets and then have an LLM craft those snippets into an answer. Think of this as a "chatbot for your documentation". Klarna, a large financial company, uses a system like this to save $40M per year on customer support costs. <br/>
•	Email chain analysis - Let's say you're an insurance company with long threads of emails between customers and insurance agents. Instead of searching through each individual email, you could retrieve relevant passages and have an LLM create strucutred outputs of insurance claims. <br/>
•	Company internal documentation chat - If you've worked at a large company, you know how hard it can be to get an answer sometimes. Why not let a RAG system index your company information and have an LLM answer questions you may have? The benefit of RAG is that you will have references to resources to learn more if the LLM answer doesn't suffice. <br/>
•	Textbook Q&A - Let's say you're studying for your exams and constantly flicking through a large textbook looking for answers to your quesitons. RAG can help provide answers as well as references to learn more. <br/>
All of these have the common theme of retrieving relevant resources and then presenting them in an understandable way using an LLM.

Slide 3: RAG Architecure <br/>
Prior to answering any question about a given document, the document is split into chunks and the chunks are indexed into a vector database (vectordb). When a question is sent to the RAG system, the top-k chunks most similar to the question are retrieved from the vector database and used to generate the answer using a large language model as generator. In order to retrieve chunks from the vector database, the question is encoded into a vector that is compared to the vector previously generated from the chunks. To prompt the generator, the question is converted into a set of instructions that instruct the LLM to find the answer within the top-k retrieved chunks.<br/>
Slide 4 and 5: <br/>
Simply chunking and embedding documents in a database and then using plain vector similarity search won’t hit the mark for multi-hop questions. Here’s why: <br/>

Repeated information in top N documents: The provided documents aren’t guaranteed to contain all the information required to answer a question fully. For example, the top three similar documents might all mention that Shariq worked at OpenAI and possibly founded a company while ignoring all the other former employees who became founders.<br/>
Missing reference information: Depending on the chunk sizes, some chunks might not contain the full context or references to the entities mentioned in the text. Overlapping the chunks can partially mitigate the issue of missing references. There are also examples where the references point to another document, so you need a co-reference resolution or preprocessing technique.<br/>
Hard to define the ideal N number of retrieved documents: Some questions require more documents for an LLM to be accurate, while in other situations, a large number of documents would only increase the noise (and cost).<br/>





