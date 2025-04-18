# MoralMind
It will make our world better 
import React, { useState } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Input } from "@/components/ui/input"; import { Button } from "@/components/ui/button"; import { Textarea } from "@/components/ui/textarea";

const ethicalFrameworks = [ { name: "Αριστοτελική Ηθική", response: "Η ειλικρίνεια είναι αρετή, όμως πρέπει να εξασκείται με φρόνηση. Αν το ψέμα είναι μικρό και στοχεύει στη φροντίδα χωρίς να προδίδει εμπιστοσύνη, ίσως είναι η φρόνιμη επιλογή." }, { name: "Καντιανή Ηθική", response: "Το ψέμα δεν μπορεί να είναι καθολικά αποδεκτό, άρα είναι ηθικά λανθασμένο, ανεξαρτήτως πρόθεσης. Πάντα οφείλεις να είσαι ειλικρινής." }, { name: "Ωφελιμισμός", response: "Αν το ψέμα μειώνει τον πόνο και δεν προκαλεί μακροπρόθεσμη ζημιά, τότε είναι προτιμότερο από την αλήθεια που πληγώνει." }, { name: "Ηθική της Φροντίδας", response: "Η φροντίδα για τον άλλο μπορεί να δικαιολογήσει ένα ψέμα, αν γίνεται με ενσυναίσθηση και όχι για να αποφύγεις ευθύνη." }, { name: "Στωική Ηθική", response: "Οφείλεις να πράττεις με αρετή ανεξαρτήτως εξωτερικών συνθηκών. Το ψέμα διαταράσσει την εσωτερική γαλήνη και άρα είναι μη επιθυμητό." }, { name: "Συμβολαιακή Ηθική", response: "Εάν το ψέμα παραβιάζει την άτυπη ή ρητή συμφωνία εμπιστοσύνης στη σχέση, είναι ηθικά εσφαλμένο. Οι ανθρώπινες σχέσεις βασίζονται σε συμφωνίες."
} ];

const dialogueQuestions = [ "Τι θα γινόταν αν εσύ ήσουν στη θέση του άλλου και μάθαινες το ψέμα;", "Πιστεύεις ότι η αγάπη θεμελιώνεται στην αλήθεια ή στην προστασία;", "Το ψέμα αυτό είναι πράξη αγάπης ή φόβου;", "Υπάρχει καλύτερη εναλλακτική από το ψέμα;", "Ποια θα ήταν η συνέπεια αυτής της πράξης σε βάθος χρόνου;" ];

export default function MoralMindApp() { const [question, setQuestion] = useState(""); const [submitted, setSubmitted] = useState(false); const [dialogue, setDialogue] = useState("");

const handleSubmit = () => { if (question.trim()) { setSubmitted(true); } };

const saveToLocalHistory = () => { const stored = localStorage.getItem("moral_mind_history") || "[]"; const updated = JSON.parse(stored); updated.unshift({ question, dialogue, timestamp: new Date().toISOString() }); localStorage.setItem("moral_mind_history", JSON.stringify(updated)); };

return ( <div className="max-w-3xl mx-auto p-6"> <h1 className="text-3xl font-bold mb-4">Ηθικός Νους</h1> <p className="mb-4 text-muted-foreground"> Γράψε ένα ηθικό ερώτημα για να το αναλύσουμε μέσα από φιλοσοφικές οπτικές. </p> <div className="flex space-x-2 mb-4"> <Input placeholder="Π.χ. Είναι σωστό να πω ψέματα για να προστατεύσω κάποιον;" value={question} onChange={(e) => setQuestion(e.target.value)} /> <Button onClick={handleSubmit}>Ανάλυση</Button> </div>

{submitted && (
    <div className="space-y-4">
      {ethicalFrameworks.map((framework, idx) => (
        <Card key={idx}>
          <CardContent className="p-4">
            <h2 className="font-semibold text-lg mb-2">{framework.name}</h2>
            <p>{framework.response}</p>
          </CardContent>
        </Card>
      ))}

      <Card>
        <CardContent className="p-4">
          <h2 className="font-semibold text-lg mb-2">Σωκρατικός Διάλογος</h2>
          <ul className="list-disc pl-5 space-y-1">
            {dialogueQuestions.map((q, i) => (
              <li key={i}>{q}</li>
            ))}
          </ul>
          <Textarea
            className="mt-4"
            placeholder="Η σκέψη μου πάνω στον διάλογο..."
            value={dialogue}
            onChange={(e) => setDialogue(e.target.value)}
          />
          <div className="text-right mt-2">
            <Button size="sm" onClick={saveToLocalHistory}>
              Αποθήκευση Συλλογισμού
            </Button>
          </div>
        </CardContent>
      </Card>
    </div>
  )}
</div>

); }

