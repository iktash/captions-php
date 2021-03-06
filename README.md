# PHP Captions
This library provides methods for working with closed caption files in a standard way from within PHP.

## Licence
MIT - See LICENCE file.

It's alway nice to hear about people using your code, so if you use this library in your code feel free to let me know. It gives me warm fuzzies and motivates me to keep writing.

## Status
### Currently working:
- Parse & Render SRT Files
- Render Dfxp (TTML) Files
- Time shift all captions from the start, or a given caption index

### To Do
- Support parsing DFXP format
- Support Shrinking and enlarging of individual caption times
- SRT Caption positioning support
- SRT & Dfxp Style Support

## Usage

### Existing Captions
	$captions = Captions::from_srt(file_get_contents("my_captions.srt"));
	// Returns instance of Captions_Set

### Captions from Scratch
	$captions = new Captions_Set;

### Adding Captions
	$caption = new Captions_Caption;
	$caption->text("And then I said, but what about the monkeys?")
		->start(0)
		->end(8.340);
	$captions->add_caption($caption);

### Altering Captions
	$captions->rewind(1.5); // Rewinds all captions 1.5 seconds

	$captions->fast_forward(2.5, 8); // Fast forwards all captions from caption #8 onwards by 2.5 seconds

### Rendering Captions

#### Caption_Set dependency
	$captions->renderer(new Captions_Renderer_SrtRenderer);
	echo $captions->render();

	// Or

	$captions->render("my_new_captions.srt");

#### Dependency free
	$renderer = new Captions_Renderer_DfxpRenderer;

	$renderer->render($captions, "my_captions.xml"); // File output parameter optional (return string)

## Tests
Tests are in the tests folder and require simpletest
	Completed 4 of 4 tests in 1.35 seconds with 0 failures
