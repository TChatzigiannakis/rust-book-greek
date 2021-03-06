|## Παράρτημα Β: Τελεστές και Σύμβολα

Το παρόν παράρτημα περιέχει ένα γλωσσάρι του συντακτικού της Rust, συμπεριλαμβανομένων
τελεστών και άλλων συμβόλων τα οποία εμφανίζονται μόνα τους ή στο πλαίσιο διαδρομών,
γενικευμένων τύπων ή συναρτήσεων, ορίων χαρακτηριστικών, μακροεντολών, γνωρισμάτων,
σχολίων, πλειάδων, και αγκίστρων.

### Τελεστές

Ο πίνακας Β-1 περιέχει τους τελετές στη Rust, ένα παράδειγμα του πώς ο τελεστής θα εμφανιζόταν
στο πλαίσιο χρήσης του, μια σύντομη επεξήγηση, και το αν ο εν λόγω τελεστής μπορεί να υπερφορτωθεί.
Εάν ο τελεστής μπορεί να υπερφορτωθεί, αναφέρεται το σχετικό χαρακτηριστικό που μπορεί να χρησιμοποιηθεί
για την υπερφόρτωσή του.

<span class="caption">Πίνακας B-1: Τελεστές</span>

| Τελεστής | Παράδειγμα | Επεξήγηση | Υπερφορτώνεται; |
|----------|---------|-------------|---------------|
| `!` | `ident!(...)`, `ident!{...}`, `ident![...]` | Επέκταση μακροεντολής | |
| `!` | `!expr` | Δυαδικό ή λογικό συμπλήρωμα | `Not` |
| `!=` | `var != expr` | Σύγρκιση ανισότητας | `PartialEq` |
| `%` | `expr % expr` | Αριθμητικό υπόλοιπο | `Rem` |
| `%=` | `var %= expr` | Αριθμητικό υπόλοιπο και ανάθεση | `RemAssign` |
| `&` | `&expr`, `&mut expr` | Δανεισμός | |
| `&` | `&type`, `&mut type`, `&'a type`, `&'a mut type` | Τύπος δείκτη δανεισμού | |
| `&` | `expr & expr` | Δυαδικό AND | `BitAnd` |
| `&=` | `var &= expr` | Δυαδικό AND και ανάθεση | `BitAndAssign` |
| `&&` | `expr && expr` | Λογικό AND | |
| `*` | `expr * expr` | Αριθμητικός πολλαπλασιασμός | `Mul` |
| `*=` | `var *= expr` | Αριθμητικός πολλαπλασιασμός και ανάθεση | `MulAssign` |
| `*` | `*expr` | Διακοπή αναφοράς | |
| `*` | `*const type`, `*mut type` | Πρωτογενής δείκτης | |
| `+` | `trait + trait`, `'a + trait` | Σύνθετος περιορισμός τύπου | |
| `+` | `expr + expr` | Αριθμητική πρόσθεση | `Add` |
| `+=` | `var += expr` | Αριθμητική πρόσθεση και ανάθεση | `AddAssign` |
| `,` | `expr, expr` | Διαχωριστικό ορισμάτων και στοιχείων | |
| `-` | `- expr` | Αριθμητική άρνηση | `Neg` |
| `-` | `expr - expr` | Αριθμητική αφαίρεση | `Sub` |
| `-=` | `var -= expr` | Αριθμητική αφαίρεση και ανάθεση | `SubAssign` |
| `->` | `fn(...) -> type`, <code>\|...\| -> type</code> | Τύπος επιστροφής συνάρτησης ή κλεισίματος | |
| `.` | `expr.ident` | Πρόσβαση σε μέλος | |
| `..` | `..`, `expr..`, `..expr`, `expr..expr` | Κυριολεκτικό διαστήματος με ανοιχτό δεξί άκρο | |
| `..=` | `..=expr`, `expr..=expr` | Κυριολεκτικό διαστήματος με κλειστό δεξί άκρο | |
| `..` | `..expr` | Συντακτικό ενημέρωσης κυριολεκτικού δομής | |
| `..` | `variant(x, ..)`, `struct_type { x, .. }` | Μοτίβο «και τα υπόλοιπα» | |
| `...` | `expr...expr` | Μέσα σε μοτίβο: περιεκτικό διάστημα | |
| `/` | `expr / expr` | Αριθμητική διαίρεση | `Div` |
| `/=` | `var /= expr` | Αριθμητική διαίρεση και ανάθεση | `DivAssign` |
| `:` | `pat: type`, `ident: type` | Περιορισμοί | |
| `:` | `ident: expr` | Απόδοση αρχικής τιμής σε πεδίο δομής | |
| `:` | `'a: loop {...}` | Ετικέτα βρόχου | |
| `;` | `expr;` | Τερματισμός πρότασης και αντικειμένου | |
| `;` | `[...; len]` | Μέρος του συντακτικού για πίνακες σταθερού μεγέθους | |
| `<<` | `expr << expr` | Αριστερόστροφη ολίσθηση | `Shl` |
| `<<=` | `var <<= expr` | Αριστερόστροφη ολίσθηση και ανάθεση | `ShlAssign` |
| `<` | `expr < expr` | Σύγκριση «μικρότερο από» | `PartialOrd` |
| `<=` | `expr <= expr` | Σύγρκιση «μικρότερο από ή ίσο με» | `PartialOrd` |
| `=` | `var = expr`, `ident = type` | Ανάθεση/ισοτιμία | |
| `==` | `expr == expr` | Σύγκριση ισότητας | `PartialEq` |
| `=>` | `pat => expr` | Μέρος του συντακτικού υποπερίπτωσης κατά το ταίριασμα | |
| `>` | `expr > expr` | Σύγκριση «μεγαλύτερο από» | `PartialOrd` |
| `>=` | `expr >= expr` | Σύγκριση «μεγαλύτερο από ή ίσο με» | `PartialOrd` |
| `>>` | `expr >> expr` | Δεξιόστροφη ολίσθηση | `Shr` |
| `>>=` | `var >>= expr` | Δεξιόστροφη ολίσθηση και ανάθεση | `ShrAssign` |
| `@` | `ident @ pat` | Ονοματοδοσία σε μοτίβο | |
| `^` | `expr ^ expr` | Δυαδικό αποκλειστικό OR | `BitXor` |
| `^=` | `var ^= expr` | Διαδικό αποκλειστικό OR και ανάθεση | `BitXorAssign` |
| <code>\|</code> | <code>pat \| pat</code> | Εναλλακτικά μοτίβων | |
| <code>\|</code> | <code>expr \| expr</code> | Δυαδικό OR | `BitOr` |
| <code>\|=</code> | <code>var \|= expr</code> | Δυαδικό OR και ανάθεση | `BitOrAssign` |
| <code>\|\|</code> | <code>expr \|\| expr</code> | Λογικό OR | |
| `?` | `expr?` | Διάδοση σφάλματος | |

### Άλλα Σύμβολα

Η παρακάτω λίστα περιλαμβάνει όλα τα μη-γράμματα που δε λειτουργούν ως τελεστές —
δηλαδή δε συμπεριφέρονται ως κλήσεις συνάρτησης ή μεταβλητής.

Ο πίνακας Β-2 δείχνει σύμβολα τα οποία εμφανίζονται μόνα τους και είναι έγκυρα σε
διάφορα σημεία.

<span class="caption">Πίνακας Β-2: Συντακτικό σε Αυτονομία</span>

| Σύμβολο | Επεξήγηση |
|--------|-------------|
| `'ident` | Ονοματισμένη διάρκεια ζωής, ή ετικέτα βρρόχου |
| `...u8`, `...i32`, `...f64`, `...usize`, etc. | Αριθμητικό κυριολεκτικό συγκεκριμένου τύπου |
| `"..."` | Κυριολεκτικό συμβολοσειράς αλφαριθμητικών |
| `r"..."`, `r#"..."#`, `r##"..."##`, etc. | Πρωτογενές κυριολεκτικό συμβολοσειράς αλφαριθμητικών, όπου οι χαρακτήρες απόδρασης δεν υπόκεινται σε επεξεργασία |
| `b"..."` | Κυριολεκτικό συμβολοσειράς από bytes — δημιουργεί `[u8]` αντί για συμβολοσειρά αλφαριθμητικών |
| `br"..."`, `br#"..."#`, `br##"..."##`, etc. | Πρωτογενές κυριολεκτικό συμβολοσειράς από bytes, συνδυασμός πρωτογενούς κυριολεκτικού και κυριολεκτικού από bytes|
| `'...'` | Κυριολεκτικό αλφαριθμητικού |
| `b'...'` | Κυριολεκτικό byte από το σύνολο ASCII |
| <code>\|...\| expr</code> | Κλείσιμο |
| `!` | Κάτω τύπος (χωρίς τιμές), για συναρτήσεις που δεν τερματίζουν |
| `_` | Μοτίβο για τις περιπτώσεις στις οποίες δε μας ενδιαφέρει η ονοματοδοσία — χρησιμοποιείται επίσης για αύξηση αναγνωσιμότητας σε ακέραια κυριολεκτικά |

Ο Πίνακας Β-3 δείχνει σύμβολα τα οποία εμφανίζονται στο πλαίσιο μιας διαδρομής
μέσα στην ιεραρχία τμημάτων προς ένα αντικείμενο.

<span class="caption">Πίνακας Β-3: Συντακτικό Σχετικό με Διαδρομές</span>

| Σύμβολο | Επεξήγηση |
|--------|-------------|
| `ident::ident` | Διαδρομή χώρου ονομάτων |
| `::path` | Διαδρομή σε σχέση με τη ρίζα του κιβωτίου (δηλ., μία ρητά απόλυτη διαδρομή) |
| `self::path` | Διαδρομή σε σχέση με το τρέχον δομοστοιχείο (δηλ., μια ρητά σχετική διαδρομή) |
| `super::path` | Διαδρομή σε σχέση με το γονέα του τρέχοντος δομοστοιχείου |
| `type::ident`, `<type as trait>::ident` | Συσχετισμένες σταθερές, συναρτήσεις, και τύποι |
| `<type>::...` | Συσχετισμένο αντικείμενο για έναν τύπο που δε μπορεί να ονοματιστεί άμεσα (π.χ., `<&T>::...`, `<[T]>::...`, κλπ.) |
| `trait::method(...)` | Αποσαφήνιση κλήσης μεθόδου ονοματίζοντας το χαρακτηριστικό το οποίο την ορίζει |
| `type::method(...)` | Αποσαφήνιση κλήσης μεθόδου ονοματίζοντας τον τύπο για τον οποίο ορίζεται |
| `<type as trait>::method(...)` | Αποσαφήνιση κλήσης μεθόδου ονοματίζοντας το χαρακτηριστικό και τον τύπο |

Ο Πίνακας Β-4 δείχνει σύμβολα τα οποία εμφανίζονται στο πλαίσιο της χρήσης
παραμέτρων γενικευμένων τύπων.

<span class="caption">Πίνακας Β-4: Γενικευμένος Προγραμματισμός</span>

| Σύμβολο | Επεξήγηση |
|--------|-------------|
| `path<...>` | Καθορίζει παραμέτρους για ένα γενικεμένο τύπο μέσα σε έναν τύπο (π.χ., `Vec<u8>`) |
| `path::<...>`, `method::<...>` | Καθορίζει παραμέτρους για ένα γενικεμένο τύπο, συνάρτηση, ή μέθοδο σε μια έκφραση - αναφέρεται συχνά ως turbofish (π.χ., `"42".parse::<i32>()`) |
| `fn ident<...> ...` | Ορίζει μια γενικεμένη συνάρτηση |
| `struct ident<...> ...` | Ορίζει μια γενικευμένη δομή |
| `enum ident<...> ...` | Ορίζει μια γενικευμένη απαρίθμηση |
| `impl<...> ...` | Ορίζει μια γενικευμένη υλοποίηση |
| `for<...> type` | Όρια διάρκειας ζωής υψηλότερου βαθμού |
| `type<ident=type>` | Ένας γενικευμένος τύπος στον οποίο ένας ή περισσότεροι συσχετισμένοι τύποι έχουν συγκεκριμένες αναθέσεις (π.χ., `Iterator<Item=T>`) |

Ο Πίνακας Β-5 δείχνει σύμβολα τα οποία εμφανίζονται στο πλαίσιο του περιορισμού
παραμέτρων γενικευμένων τύπων με χρήση χαρακτηριστικών ως όρια.

<span class="caption">Πίνακας Β-5: Περιορισμοί με Χαρακτηριστικά ως Όρια</span>

| Σύμβολο | Επεξήγηση |
|--------|-------------|
| `T: U` | Ο γενικευμένος τύπος `T` περιορίζεται σε τύπους οι οποίοι υλοποιούν το `U` |
| `T: 'a` | Ο γενικευμένος τύπος `T` πρέπει να ζει περισσότερο από τη διάρκεια ζωής `'a` (εννοώντας ότι ο τύπος δε μπορεί μεταβατικά να περιέχει αναφορές σε διάρκειες ζωής μικρότερες από την `'a`) |
| `T : 'static` | Ο γενικευμένος τύπος `T` δεν περιέχει δανεισμένες αναφορές παρά μόνον όσες έχουν διάρκεια ζωής `'static` |
| `'b: 'a` | Η γενικευμένη διάρκεια ζωής `'b` πρέπει να διαρκεί περισσότερο από τη διάρκεια ζωής `'a` |
| `T: ?Sized` | Παραχώρηση στην παράμετρο γενικευμένου τύπου της δυνατότητας να αναφέρεται σε τύπο με δυναμικό μέγεθος |
| `'a + trait`, `trait + trait` | Σύνθετος περιορισμός τύπου |

Ο Πίνακας Β-6 δείχνει σύμβολα τα οποία εμφανίζονται στο πλαίσιο της κλήσης
ή του ορισμού μακροεντολών και καθορισμού γνωρισμάτων σε ένα στοιχείο.

<span class="caption">Πίνακας Β-6: Μακροεντολές και Γνωρίσματα</span>

| Σύμβολο | Επεξήγηση |
|--------|-------------|
| `#[meta]` | Εξωτερικό γνώρισμα |
| `#![meta]` | Εσωτερικό γνώρισμα |
| `$ident` | Υποκατάσταση μακροεντολής |
| `$ident:kind` | Αιχμαλώτιση μακροεντολής |
| `$(…)…` | Επανάληψη μακροεντολής |

Ο Πινακας Β-7 δείχνει σύμβολα τα οποία δημιουργούν σχόλια.

<span class="caption">Πίνακας Β-7: Σχόλια</span>

| Σύμβολο | Επεξήγηση |
|--------|-------------|
| `//` | Σχόλιο μίας γραμμής |
| `//!` | Εσωτερικό σχόλιο τεκμηρίωσης μίας γραμμής |
| `///` | Εξωτερικό σχόλιο τεκμηρίωσης μίας γραμμής |
| `/*...*/` | Σχόλιο πολλών γραμμών |
| `/*!...*/` | Εσωτερικό σχόλιο τεκμηρίωσης πολλών γραμμών |
| `/**...*/` | Εξωτερικό σχόλιο τεκμηρίωσης πολλών γραμμών |

Ο Πίνακας Β-8 δείχνει σύμβολα τα οποία εμφανίζονται στο πλαίσιο της χρήσης πλειάδων.

<span class="caption">Πίνακας Β-8: Πλειάδες</span>

| Σύμβολο | Επεξήγηση |
|--------|-------------|
| `()` | Άδεια πλειάδα (γνωστή και ως τύπος μονάδας), υποδηλώνει και το κυριολεκτικό αλλά και τον αντίστοιχο τύπο |
| `(expr)` | Έκφραση σε παρένθεση |
| `(expr,)` | Έκφραση πλειάδας ενός στοιχείου |
| `(type,)` | Τύπος πλειάδας ενός στοιχείου |
| `(expr, ...)` | Έκφραση πλειάδας |
| `(type, ...)` | Τύπος πλειάδας |
| `expr(expr, ...)` | Έκφραση κλήσης συνάρτησης — χρησιμοποιείται επίσης για την απόδοση αρχικών τιμών σε πλειάδες `struct`s και παραλλαγές πλειάδων `enum` |
| `ident!(...)`, `ident!{...}`, `ident![...]` | Κλήση μακροεντολής |
| `expr.0`, `expr.1`, κλπ. | Προσπέλαση πλειάδας |

Ο Πίνακας Β-9 δείχνει τα πλαίσια στα οποία χρησιμοποιούνται άγκιστρα.

<span class="caption">Πίνακας Β-9: Άγκιστρα</span>

| Πλαίσιο | Επεξήγηση |
|---------|-------------|
| `{...}` | Έκφραση μπλοκ |
| `Type {...}` | Κυριολεκτικό `struct` |

Ο Πίνακας Β-10 δείχνει τα πλαίσια στα οποία οι χρησιμοποιούνται αγκύλες.

<span class="caption">Πίνακας Β-10: Αγκύλες</span>

| Πλαίσιο | Επεξήγηση |
|---------|-------------|
| `[...]` | Κυριολεκτικό πίνακα |
| `[expr; len]` | Κυριολεκτικό πίνακα που περιέχει `len` φορές την έκφραση `expr` |
| `[type; len]` | Τύπος πίνακα που περιέχει `len` πλήθος στοιχείων τύπου `type` |
| `expr[expr]` | Προσπέλαση συλλογής. Μπορεί να υπερφορτωθεί (`Index`, `IndexMut`) |
| `expr[..]`, `expr[a..]`, `expr[..b]`, `expr[a..b]` | Προσπέλαση συλλογής που παριστάνει την τμηματοποιήση συλλογής, με χρήση `Range`, `RangeFrom`, `RangeTo`, ή `RangeFull` ως «ευρετήριο» |
