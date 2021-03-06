## Παράρτημα Γ: Κληρονομικότητα Χαρακτηριστικών

Σε διάφορα σημεία του βιβλίου, συζητήσαμε το γνώρισμα `derive`, το οποίο μπορείτε
να εφαρμόσετε σε έναν ορισμό μιας δομής ή μιας απαρίθμησης. Το γνώρισμα `derive`
γεννά κώδικα ο οποίος υλοποιεί ένα χαρακτηριστικό με μια προεπιλεγμένη υλοποίηση
στον τύπο ο οποίος υποσημειωθηκε με το `derive`.

Στο παρόν παράρτημα, αναφέρουμε όλα τα χαρακτηριστικά στη βασική βιβλιοθήκη τα
οποία μπορείτε να χρησιμοποιήσετε με το `derive`. Κάθε ενότητα καλύπτει:

* Ποιους τελεστές και ποιες μεθόδους καθιστά διαθέσιμους η κληρονομικότητα του
  χαρακτηριστικού με χρήση του `derive`
* Τι κάνει η υλοποίηση που προσφέρεται από το `derive`
* Τι σηματοδοτεί για τον τύπο η υλοποίηση του χαρακτηριστικού
* Τις συνθήκες στις οποίες επιτρέπεται ή δεν επιτρέπεται να υλοποιείται αυτό το
  χαρακτηριστικό
* Παραδείγματα λειτουργιών που απαιτούν το χαρακτηριστικό

Αν θέλετε διαφορετική συμπεριφορά από αυτήν που προσφέρεται από το γνώρισμα
`derive`, συμβουλευτείτε την [τεκμηρίωση της βασικής βιβλιοθήκης](../std/index.html)<!-- ignore -->
για κάθε χαρακτηριστικό, ώστε να βρείτε λεπτομέρειες σχετικά με το πώς
να τα υλοποιήσετε μη αυτόματα.

Τα υπόλοιπα χαρακτηριστικά που ορίζονται στη βασική βιβιλιοθήκη δε μπορούν να
υλοποιηθούν για τους τύπους σας με χρήση του `derive`. Για εκείνα τα χαρακτηριστικά
δε θα είχε νόημα κάποια προεπιλεγμένη συμπεριφορά, επομένως αφήνεται σε εσάς να τα
υλοποιήσετε με έναν τρόπο που έχει νόημα για το σκοπό για τον οποίο τα προορίζετε.

Ένα παράδειγμα χαρακτηριστικού που δε μπορεί να υλοποιηθεί αυτόματα είναι το
`Display`, το οποίο διαχειρίζεται τη διαμόρφωση μιας τιμής για τον τελικό χρήστη.
Θα πρέπει πάντα να σκέφτεστε το σωστό τρόπο να παρουσιάσετε έναν τύπο στον τελικό
χρήστη. Ποια μέρη του τύπου θα πρέπει να επτρέπεται να δει ο τελικός χρήστης; Ποια
μορφή των δεδομένων θα είναι πιο χρήσιμη στο χρήστη; Ο μεταγλωττιστής της Rust δεν
έχει αυτές τις γνώσεις, επομένως δε μπορεί να προσφέρει μια ταιριαστή προεπιλεγμένη
συμπεριφορά για εσάς.

Η λίστα με τα κληρονομήσιμα χαρακτηριστικά που προσφέρεται σε αυτό το παράρτημα δεν
είναι πλήρως περιεκτική: διάφορες βιβλιοθήκηες μπορούν να υλοποιούν το `derive` για
τα δικά τους χαρακτηρστικά, καθιστώντας ανοιχτό το σύνολο των χαρακτηριστικών με τα
οποία μπορεί να χρησιμοποιηθεί το `derive`. Η υλοποίηση του `derive` περιλαμβάνει τη
χρήση μιας διαδικαστικής μακροεντολής, η οποία καλύπτεται στην ενότητα «Μακροεντολές»
του Κεφαλαίου 19.

### `Debug` για Έξοδο για Χρήση από τον Προγραμματιστή

Το χαρακτηριστικό `Debug` προσφέρει τη δυνατότητα διαμόρφωσης σε μορφή κατάλληλη για
αποσφαλμάτωση, η οποία μπορεί να υποδειχθεί προσθέτοντας `:?` μέσα σε εντολείς θέσης
`{}`.

Το χαρακτηριστικό `Debug` σας επιτρέπει να τυπώνετε στιγμιότυπα ενός τύπου με σκοπό
την αποσφαλμάτωση, ώστε εσείς και άλλοι προγραμματιστές οι οποίοι χρησιμοποιούν τον
τύπο σας να μπορούν να μελετήσουν το στιγμιότυπο σε κάποια συγκεκριμένη στιγμή κατά
την εκτέλεση του προγράμματος.

Το χαρακτηριστικό `Debug` απαιτείται, για παράδειγμα, στη χρήση της μακροεντολής
`assert_eq!`. Η συγκεκριμένη μακροεντολή τυπώνει τις τιμές των στιγμιοτύπων που της
μεταβιβάζονται ως ορίσματα εάν ο ισχυρισμός ισότητας διαψευστεί, έτσι ώστε οι
προγραμματιστές να μπορούν να δουν γιατί τα δύο στιγμιότυπα δεν ήταν ίσα.

### `PartialEq` και `Eq` για Συγκρίσεις Ισότητας

Το χαρακτηριστικό `PartialEq` σας επιτρέπει να συγκρίνετε στιγμιότυπα ενός τύπου για
να ελεγχθούν για ισότητα και καθιστά δυνατή τη χρήση των τελεστών `==` και `!=`.

Η κληρονόμηση του `PartialEq` παρέχει υλοποίηση της μεθόδου `eq`. Όταν το `PartialEq`
κληρονομείται από δομές, δύο στιγμιότυπα είναι ίσα μόνο αν *όλα* τα πεδία τους είναι ίσα,
και τα στιγμιότυπα είναι άνισα εάν οποιαδήποτε πεδία τους είναι άνισα. Όταν κληρονομείται
από απαριθμήσεις, κάθε παραλλαγή είναι ίση με τον εαυτό της και άνιση με κάθε άλλη
παραλλαγή.

Το χαρακτηριστικό `PartialEq` απαιτείται, για παράδειγμα, στη χρήση της μακροεντολής
`assert_eq!`, η οποία πρέπει να μπορεί να συγκρίνει δύο στιγμιότυπα ενός τύπου για
ισότητα.

Το χαρακτηριστικό `Eq` δεν έχει μεθόδους. Σκοπός του είναι να σηματοδοτεί ότι κάθε
τιμή που το υλοποιεί είναι ίση με τον εαυτό της. Το χαρακτηριστικό `Eq` μπορεί να εφαρμοστεί μόνο σε τύπους που υλοποιούν και το `PartialEq`, αν και δε μπορούν
απαραίτητα όλοι οι τύποι που υλοποιούν το `PartialEq` να υλοποιήσουν και το
`Eq`. Ένα παράδειγμα είναι οι αριθμοί κινητής υποδιαστολής: η υλοποίηση των αριθμών
κινητής υποδιαστολής δηλώνει ότι δύο στιγμιότυπα της τιμής not-a=number (`NaN`) δεν
είναι ίσα μεταξύ τους.

Ένα παράδειγμα του πότε το `Eq` απαιτείται είναι για κλειδιά σε ένα `HashMap<K, V>`,
έτσι ώστε το `HashMap<K, V>` να μπορεί να ελέγξει αν δύο κλειδιά είναι ίσα.

### `PartialOrd` και `Ord` για Συγκρίσεις Διάταξη

Το χαρακτηριστικό `PartialOrd` σας επιτρέπει να συγκρίνετε στιγμιότυπα ενός τύπου
για λόγους διάταξης. Ένας τύπος που υλοποιεί το `PartialOrd` μπορεί να
χρησιμοποιηθεί με τους τελεστές `<`, `>`, `<=`, και `>=`. Μπορείτε να εφαρμόσετε το
χαρακτηριστικό `PartialOrd` μόνο σε τύπους που υλοποιούν και το `PartialEq`.

Η κληρονόμηση του χαρακτηριστικού `PartialOrd` προσφέρει υλοποίηση της μεθόδου
`partial_cmp`, η οποία επιστρέφει ένα `Option<Ordering>` το οποίο θα είναι `None`
όταν οι τιμές δε μπορούν να παράξουν διάταξη. Ένα παράδειγμα τιμής που δεν παράγει
διάταξη, παρόλο που οι περισσότερες τιμές αυτού του τύπου μπορούν να συγκριθούν,
είναι η τιμή not-a-number (`NaN`) των αριθμών κινητής υποδιαστολής. Η κλήση της
`partial_cmp` με ορίσματα οποιονδήποτε αριθμό κινητής υποδιαστολής και την τιμή
`NaN` θα επιστρέψει `None`.

Όταν κληρονομείται από δομές, η `PartialOrd` συγκρίνει δύο στιγμιότυπα συγκρίνοντας
την τιμή κάθε πεδίου, με τη σειρά με την οποία τα πεδία εμφανίζονται στον ορισμό
της δομής. Όταν κληρονομείται από απαριθμήσεις, οι παραλλαγές οι οποίες δηλώνονται
νωρίτερα στον ορισμό της απαρίθμησης θεωρούνται μικρότερες από τις παραλλαγές που
δηλώνονται αργότερα.

Το χαρακτηριστικό `PartialOrd` απαιτείται, για παράδειγμα, για τη μέθοδο `gen_range`
του κιβωτίου `rand` το οποίο δημιουργεί μια τυχαία τιμή σε ένα εύρος το οποίο
καθορίζεται από μία ελάχιστη και μία μέγιστη τιμή.

Το χαρακτηριστικό `Ord` σας επιτρέπει να γνωρίζετε ότι υπάρχει μια έγκυρη διάταξη
για κάθε ζεύγος τιμών του τύπου ο οποίος το υλοποιεί. Το χαρακτηριστικό `Ord`
υλοποιεί τη μέθοδο `cmp`, η οποία επιστρέφει ένα `Ordering` αντί για
`Option<Ordering>`, εφόσον πάντοτε υπάρχει μια έγκυρη διάταξη. Μπορείτε να
εφαρμόσετε το χαρακτηριστικό `Ord` μόνο σε τύπους οι οποίοι υλοποιούν το `PartialOrd`
και το `Eq` (το οποίο με τη σειρά του απαιτεί το `PartialEq`). Όταν κληρονομείται
από δομές και απαριθμήσεις, η `cmp` συμπεριφέρεται όπως η `partial_cmp` για το
`PartialOrd`.

Ένα παράδειγμα όπου απαιτείται το `Ord` είναι η αποθήκευση τιμών σε ένα `BTreeSet<T>`,
μια δομή δεδομένων η οποία αποθηκεύει δεδομένα βάσει της σειράς διάταξης των τιμών.

### `Clone` και `Copy` για Διπλασιασμό Τιμών

Το χαρακτηριστικό `Clone` σας επιτρέπει να δημιουργείτε ρητά ένα βαθύ αντίγραφο
μιας τιμής, και η διαδικασία αντιγραφής μπορεί να περιέχει οποιοδήποτε κώδικα,
καθώς και αντιγραφή δεδομένων από και προς το σωρό. Δείτε την ενότητα «Τρόποι Αλληλεπίδρασης Μεταβλητών και Δεδομένων: Clone» στο Κεφάλαιο 4 για περισσότερες
πληροφορίες για το `Clone`.0

Η κληρονόμηση του `Clone` υλοποιεί τη μέθοδο `clone`, η οποία όταν είναι
υλοποιημένη για ολόκληρο τον τύπο, καλεί την `clone` κάθε ενός από τα μέρη του
τύπου. Αυτό σημαίνει ότι για να κληρονομήσει ένας τύπος το `Clone`, θα πρέπει όλα
τα πεδία ή οι τιμές του να υλοποιούν το `Clone`.

Ένα παράδειγμα όπου απαιτείται το `Clone` είναι όταν καλείτε τη μέθοδο `to_vec` σε
ένα τμήμα (slice). Ένα τμήμα δεν έχει κυριότητα των στιγμιοτύπων τα οποία περιέχει, αλλά
το διάνυσμα που επιστρέφεται από την `to_vec` θα πρέπει να έχει κυριότητα των
στιγμιοτύπων, επομένως η `to_vec` καλεί την `clone` σε κάθε αντικείμενο. Έτσι, ο τύπος
που αποθηκεύεται στο τμήμα πρέπει να υλοποιεί το `Clone`.

Το χαρακτηριστικό `Copy` σας επιτρέπει να διπλασιάσετε μια τιμή αντιγράφοντας απλά
τη δυαδική της αναπαράσταση στη στοίβα – δεν απαιτείται ειδικός κώδικας. Δείτε την
ενότητα «Δεδομένα Μόνο στη Στοίβα: Copy» στο Κεφάλαιο 4 για περισσότερες πληροφορίες για
την `Copy`.

Το `Copy` δεν ορίζει μεθόδους, έτσι ώστε να εμποδίζει τους προγραμματιστές από τυχόν
απόπειρα να τις υπερφορτώσουν και άρα να παραβιάσουν την υπόθεση ότι δεν εκτελείται άγνωστος κώδικας κατά την αντιγραφή. Με αυτό τον τρόπο, όλοι οι προγραμματιστές μπορούν
να υποθέσουν ότι η αντιγραφή μιας τιμής γίνεται πολύ γρήγορα.

Μπορείτε να κληρονομήσετε το `Copy` σε κάθε τύπο του οποίου όλα τα μέρη υλοποιούν το
`Copy`. Μπορείτε να εφαρμόσετε το `Copy` μόνο σε τύπους οι οποίοι υλοποιούν το `Clone`,
γιατί ένας τύπος που υλοποιεί το `Copy` έχει μία τετριμμένη υλοποίηση του `Clone` η
οποία κάνει το ίδιο πράγμα με το `Copy`.

Το χαρακτηριστικό `Copy` σπάνια χρειάζεται – τύποι οι οποίοι υλοποιούν το `Copy` έχουν
πρόσβαση σε κάποιες βελτιστοποιήσεις, που σημαίνει ότι δε χρειάζεται να καλέσετε το
`clone`, πράγμα το οποίο κάνει τον κώδικα συντομότερο.

Οτιδήποτε μπορεί να επιτευχθεί με την `Copy` μπορεί να επιτευχθεί με την `Clone`, αλλά ο
κώδικας μπορεί να είναι πιο αργός ή να χρειαστεί να χρησιμοποιηθεί το `clone` σε κάποια
σημεία.

### `Hash` για Αντιστοίχιση Τιμής σε Τιμή Σταθερού Μεγέθους

Το χαρακτηριστικό `Hash` σας επιτρέπει να πάρετε ένα στιγμιότυπο ενός τύπου οποιουδήποτε
μεγέθους και να το αντιστοιχίσετε σε ένα στιγμιότυπο μιας τιμής σταθερού μεγέθους με χρήση
μιας συνάρτησης κατατεμαχισμού. Η κληρονόμηση του `Hash` υλοποιεί τη μέθοδο `hash`. Η
κληρονομούμενη υλοποίηση της μεθόδου `hash` συνδυάζει το αποτέλεμσα της κλήσης της `hash`
σε κάθε μέρος του τύπου, πράγμα που σημαίνει ότι όλα τα πεδία ή οι τιμές πρέπει επίσης να
υλοποιούν το `Hash` προκειμένου να κληρονομεί ένας τύπος το `Hash`.

Ένα παράδειγμα όπου το `Hash` είναι απαραίτητο είναι η αποθήκευση κλειδιών σε ένα
`Hash<K, V>` για αποδοτική αποθήκευση δεδομένων.

### `Default` για Προεπιλεγμένες Τιμές

Το χαρακτηριστικό `Default` σας επιτρέπει να δημιουργήσετε μια προεπιλεγμένη τιμή για έναν
τύπο. Η κληρονόμηση του `Default` υλοποιεί τη συνάρτηση `default`. Η κληρονομούμενη
υλοποίηση της συνάρτηση `default` καλεί τη συνάρτηση `default` κάθε μέρους του τύπου, πράγμα
που σημαίνει ότι όλα τα πεδία και οι τιμές πρέπει επίσης να υλοποιούν το `Default`
προκειμένου να κληρονομεί ένας τύπος το `Default`.

Είναι συνηθισμένο η συνάρτηση `Default::default` χρησιμοποιείται σε συνδυασμό με το
συντακτικό ενημέρωσης δομής το οποίο συζητήθηκε στην ενότητα «Δημιουργώντας Στιγμιότυπα
Από Άλλα Στιγμιότυπα με Χρήση του Συντακτικού Ενημέρωσης Δομής» στο Κεφάλαιο 5. Μπορείτε να
προσαρμόσετε μερικά πεδία μιας δομής και μετά να θέσετε και να χρησιμοποιήσετε μια
προεπιλεγμένη τιμή για τα υπόλοιπα πεδία με χρήση του `..Default::default()`.

Το `Default` απαιτείται όταν χρησιμοποιείτε τη μέθοδο `unwrap_or_default` σε στιγμιότυπα
τύπου `Option<T>`, για παράδειγμα. Εάν το `Option<T>` είναι `None`, η μέθοδος
`unwrap_or_default` θα επιστρέψει το αποτέλεσμα της `Default::default` για τον τύπο `T` του
`Option<T>`.
