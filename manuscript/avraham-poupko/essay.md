#   Ubiquitous Language - More Than Just Shared Vocabulary (by Avraham Poupko)
A key tenant of DDD is _ubiquitous language_, and rightfully so. DDD is about improving domain communication and understanding. What better way to improve understanding than to make sure that we all speak the same language, and use the same words to describe the same things? In this paper, I use some insights and concepts from the study of how language is used, to explain in some detail how it is that ubiquitous language provides shared understanding.

The term ubiquitous language is often used to mean "shared vocabulary". It is important to put emphasis on the word _language_ in “ubiquitous language” to make the point that we need to expand our understanding of the term ubiquitous language to include not only the words we use, but how  we use them.

## The importance of language
Language is so much a
part of our lives that we sometimes tend to overlook its power and complexity. We just assume that language is there so that we can talk to each other. The truth is that the use of language is one of the most complex human activities. And proper understanding of language allows us to gain deep insights into our humanity. Here is a quick overview of why language is so important to us.

### Cooperation comes from communication
Any non-trivial man-made system is always the result of cooperation. No system of any complexity has ever been created by one person. Cooperation cannot happen without communication and for communication to happen we need language. We need to have a way to communicate 
thoughts so that when I have a certain idea or thought in my mind, I can invoke that thought or idea in your mind. Once we have the same thought, the same vision of what is, what can be and how we get there, we can start cooperating. 

## Theory of Language
To better appreciate the importance of ubiquitous language, it is worth while diving a bit more into some language theory and how language is used. Particularly, I would like to focus on how we use language to communicate complicated and complex ideas.
### Words vs. Concepts
Let’s call those ideas that we wish to communicate to each other _concepts_. Words themselves are not concepts, but our brain is able to translate words into concepts. Even though people write and talk in _words_, they think in _concepts_. We know this to be true because people who cannot use verbal or oral language (such as infants, people that have suffered a traumatic injury or blind-deaf people that have not been exposed to language) are still capable of thought. They may struggle to communicate and express these thoughts because they do not have language, but they certainly have these thoughts. When I struggle to find words to properly explain an idea, or when I say "words cannot express what I feel", I am saying that there are some thoughts or emotions that are very real, but that do not easily lend themselves to verbal expression. It might be true that language is critical for developing extensive concepts and abstract thinking, nonetheless many cognitive scientists agree that we do not need language in order to think.

Because we do not know how to communicate in concepts, we need a "communication layer". I think something, imagine something or even feel something which I communicate to you in words. I hope that when you hear those words, the image I have in my mind will be invoked in your mind. In order for this to happen effectively, we need to share a common mapping of words to concepts. The more consistent we are with the way we use words, the more likely it is that the mapping from words to concepts is as expected.

### Language is more than just words
On their own, words are sequenced in a rather one dimensional way. When speaking or writing, a word can come before or after other words. How is it that we can communicate such rich and complex ideas using only words? More so, words are relatively simple to utter and to understand. Thoughts are complex. How then do we communicate complex thoughts using simple words? 
The main answer is _syntax_. It is syntax that allows us to combine simple words together and to express complex thoughts. In the words of the great language scholar Steven Pinker:
_Syntax is complex, but the complexity is there for a reason. For our thoughts are surely even more complex, and we are limited by a mouth that can pronounce a single word at a time._

Simply put "syntax" is "the set of rules, principles, and processes that govern the structure of sentences". However, that is a gross 
oversimplification. It is syntax that allows me to express arbitrarily complex thoughts and ideas using simple words, just by organizing them. Consider, for example the simple yet profound statement by Kafka: "A wet man does not fear the rain.” This is a statement about human nature that uses imagery, symbolism and metaphor yet is comprised of very simple and well known words.
So, when we use a ubiquitous language, we are not only agreeing on the meaning of words, but we are using syntax to communicate the complexities of the system that we are creating.

#### Syntax provides for the exchange of complex ideas
We can imagine a group of creative people that want to exchange ideas with each other, and perhaps come up with new ideas. As the conversation goes on, the ideas that these people are discussing are becoming more and more complex. If they all speak the same language and share the same vocabulary, then they can express extremely complex ideas using syntax. However, if they do not speak the same language, or do not share the same vocabulary, these people are extremely limited in what they can express, and syntax won't help.  While a shared vocabulary is a critical element needed for the discussion of complex ideas, it is syntax that actually enables the complex communication to take place.

Let's say for example that in our domain we use the concept of "invoice". This is a real world concept that as a noun means a demand for payment for a service rendered or goods delivered, and as a verb in means the delivering of the demand to a customer.
But there is quite a bit of nuance here. Even as a noun, "invoice" can mean the demand for payment, or it can mean the paper or email representing the demand. I can say "we need to create an invoice for that customer" and mean many things. It can mean that we need to print up the paper, or that we need to calculate how much he owes so that we can demand the payment.
When designing billing software, "invoice" might be a database record representing the sum owed, or a PDF that we need to mail to the customer, or it can mean the actual email that we mailed. We will need to find words for an invoice that has been created, but not sent, and an invoice that has been sent, but not settled, and an invoice that has been settled. The more we talk about invoices the more we will understand each other. So when I say:
"I think we will not be ready to deliver 'invoice'. The creation of the invoice fails if one of the line items contains a reference to a different currency", the rest of the team members will know exactly what I mean. 

#### Learning language is about learning syntax
Watching children learning to communicate we observe something astounding. Children learn new words from their environment, and are then able to use that vocabulary to articulate complex ideas using sentences that they have never heard before. This continues throughout our lives. We use a fixed and limited vocabulary and a fixed set of syntax rules to utter sentences that are truly unique. Each and every one of has said countless sentences that have never before been said, and might never be said again. Here too we see that while we need common words to express our creativity, our expression of creative thought happens mainly through syntax. As designers and developers, when we are able to express _new_ ideas and create _new_ sentences using the agreed on ubiquitous language, we can say that we are masters of the language, or at least proficient in it.

### Levels of Communication
Words have multiple meanings. I am not referring to homonyms and homographs (words that sound alike or that are spelled alike but have different meanings). I am referring to the same word with its dictionary definition, but that invokes a different image, idea or concept. We might use the word _semantics_ to refer to the meaning of the word. 

Words have at least three levels of meaning.
#### Denotation
Denotation is the explicit literal meaning as defined by a dictionary. (Sometimes called "a direct representation of a simple real world idea").
#### Connotation
Cultural and emotional meanings that a word might have. These are sometimes taken to be positive or negative. 
#### Association
Words will also evoke certain thoughts or ideas by association. These are not necessarily cultural, rather they are dependent on the particular experiences of the speaker and audience.
When we use language to discuss the complexities of the system, we are using all levels of meaning. So we are not just using words with their dictionary denotation, we are also using connotation and association. It is important that when we use the same words, we are aware of those different levels of meaning, because it is those levels of meaning that allow deep and complex conversation to take place.

### "Invoice" as an example
For example, lets look once again at the noun "invoice".
Its denotation is a "demand for payment" or perhaps a digital representation of a demand for payment. But that might not capture all the nuance of the word invoice. Reading that definition, I might feel that I only issue an invoice of the customer does not pay on his own.
The connotation of the word "invoice" might be the knowledge that customers do not pay until invoiced. Not because they are trying to get away without paying, but because that is how business works. An invoice is not something you issue after the customer has refused to pay, it is something that every transaction must have in order for the business to run properly.
In my particular group the word "invoice" carries an association of criticality and complexity. If the invoicing has a mistake, the business suffers. If the invoice does not link properly to the audit trail, we might all be called in for investigation. This association was created in part when I delivered an invoice module with a small flaw that miscalculated the tax due. I lost customer trust, missed a chance at promotion, and was lucky I did not get fired. 
So when my team hears the word "invoice", we get serious.

As you can see, when we talk about invoice, there are many levels of meaning at work that come together and allow us to create a common 
understanding of what "invoice" means.

## A dictionary is not enough

### How do we use language? 
In the world of system design, language is not only used to _describe_ the system, it is used to _discuss_ the system. This is an important distinction. When I am describing a system, I have a clear image in my mind, and I am using language to describe it to you, so that you will have that image in your mind. However, when we are discussing a system, we each have a different perspective or understanding of the system as well as a different mental model. As the discussion progresses, the two models start converging to one model, and the meaning and uses of the words at all levels start converging as well. The more we discuss the model using the same words, the more those words will evoke the same images in our minds.
### Learning a new language 
How do we learn a new language? A real bad way to learn a new language is to learn from a dictionary. The dictionary will teach you the meanings of words, but it will not teach you how to use those words properly. In order to really learn a language, you must talk with other people who use the language and see how they use the words in different sentences and different situations. You must try speaking words yourself and see how other speakers of the language respond to the way you use them in sentences. You will see what syntaxes are useful in conveying your meaning. If you are part of a group or community, you will discover that over time, words start developing their own context-dependent connotations and associations. 

The same applies when we are learning a new domain. Learning a new domain is not only learning the domain objects and the relationships between them. As Eric Evans points out, learning a new domain includes learning the proper names for the domain objects and relationships. I argue that it includes even more. Learning a new domain also means the evolving of a language in the wider sense of the word. A language that includes all the connotations and associations, as well as syntax rules that allow us to have deep and meaningful conversations about the domain.
## In summary
Domain Driven Design has truly revolutionized the way we think and talk about domains, domain problems and the solutions to those problem. A critical component in Domain Driven Design is ubiquitous language. The power of ubiquitous language is not just in giving a common meaning to words, it is in being aware of and making use of the complexities of language. If we understand those complexities, we will be better communicators. 
I believe that a deeper study of the theory of language by Domain Driven Design practitioners will advance Domain Driven Design. By better understanding how human communication works, we can better communicate. Better communication always leads to better design.


