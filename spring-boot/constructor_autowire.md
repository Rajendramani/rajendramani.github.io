பொதுவாக spring-இல் மூன்று வகையான Injection-கள் பயன்படுத்தப்படுகின்றன 

1. Field Injection (@Autowire)
    
2. Setter Injection 
    
3. Constructor Injection (Spring officially preferred) 
    

இதில் எதை பயன்படுத்தினாலும் அது 100% வேலைசெய்யும், ஆனால் design wise எது சரி? 

Spring officially ஏன் Constructor injection ஐ preferred செய்கிறது? 

இது  எது சரியான code என்பதைப்பற்றி இல்லை. 
It's about working code vs correct design code. 

பொதுவாக Controller class இல் நாம் @Autowire ஐ பயன்படுத்துகிறோம் என்றால், 

- Controller class இல் எந்த business logic யும் இருக்காது.
    
- Unit-test இல் controller class cover செய்யப்படமாட்டாது.
    

Service class இல் அப்படி இல்லை, மேலே சொன்ன இரண்டு points ஐயும் cover செய்வவோம். 

உதாரணமாக, 

```
@Service

public class NoteService { 

  

@Autowire 

private NoteRepository noteRepository;

private void doSomething(){

noteRepository.getById(...);

}

  

}
```

  

இது எப்படி செயல்படுத்தப்படுகிறது என்று பார்ப்போம்:

1. Constructor மூலமாக NoteService() object உருவாக்க படுகிறது. 
    
2. பின், noteRepository==null என்று noteRepository object உருவாக்க படுகிறது. 
    
3. Reflection மூலம் noteRepository field value வை inject செய்கிறது. 
    

  

> [!NOTE]
> 
> இதில் ஒரு சர்ச்சை இருக்கிறது. இந்த noteRepository injection ஆனது NoteService object உருவானத்துக்கு பிறகு நடக்கிறது. ஆனால் design படி dependency object உருவான பிறகுதான் target object உருவாக வேண்டும். 

சுருக்கமாக சொல்லப்போனால், அடுப்பை பற்ற வைத்த பிறகு கடுகு, உளுந்தப் பருப்பு ஐ தேட கூடாது. தேவையான ingredients ஐ எடுத்த பிறகு தான் அடுப்பை பற்ற வைக்க வேண்டும். 
 

இதில் dependency என்பது  noteRepository ஐ குறிக்கிறது. 

Target object என்பது NoteService ஐ குறிக்கிறது. 

  

NoteRepository இல்லாமல் NoteService உருவாகி என்ன பயன்? 

மேலும் அது உருவாகிறதா இல்லையா என்று developer க்கு எப்படி தெரியும்? 

Run time இல் தான் தெரியவரும். 

  

சரி, Constructor Injection எப்படி செயல்படுகிறது என்று பார்ப்போம், 

```
@Service

public class NoteService { 

  

private final NoteRepository noteRepository;

public NoteService(NoteRepository noteRepository){

this.noteRepository=noteRepository;

}

private void doSomething(){

noteRepository.getById(...);

}

  

}
```

  

> [!NOTE]
> இதில் constructor மூலமாக NoteService உருவாகிறது. ஆனால் உருவாகும் போதே அதனுடைய dependency object ஆனா  noteRepository தேவைப்படுகிறது. 
> 
> மேலும், முக்கியமாக இந்த dependency  இல்லை என்றால் NoteService object உருவாக முடியாது. App startup இல் fail ஆகிவிடும். 

  

சரி இப்போ without final என்று குறிப்பிட்டால் என்ன ஆகும் ? 

`private NoteRepository noteRepository;`

By the mistake, 

```
this.noteRepository = null;

this.noteRepository = anotherRepository; 
```

என்று கொடுக்க வாய்ப்பு இருக்கிறது. எனவே noteRepository object ஐ மாற்ற முடியாதபடி வைக்கவேண்டும் அதாவது immutable ஆகா. அதற்குத்தான் இந்த final keyword.