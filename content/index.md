---
seo:
  title: Laravel REST API Flutter
  description: A Flutter package to integrate cleanly with a Laravel REST API backend.
---
::u-page-hero
---
orientation: horizontal
---
  :::gif-player
  :::

#title
Laravel REST API – Flutter

#description
A Flutter package that provides a clean, typed integration between your Flutter app and a Laravel REST API backend: custom HTTP client, repositories, search, mutations, deletes, and custom actions.

  :::prose-pre
  ---
  code: flutter pub add laravel_rest_api_flutter
  filename: Terminal
  ---
  ```bash
   flutter pub add laravel_rest_api_flutter
  ```
  :::

#links
  :::u-button
  ---
  to: /getting-started/introduction
  size: xl
  trailing-icon: i-lucide-arrow-right
  ---
  Get Started
  :::
#links
  :::u-button
  ---
  to: https://pub.dev/packages/laravel_rest_api_flutter
  size: xl
  color: neutral
  target: _blank
  icon: i-simple-icons-dart
  ---
  Pub.dev
  :::
#links
  :::u-button
  ---
  to: https://github.com/xefi/laravel-rest-api-flutter
  size: xl
  color: neutral
  target: _blank
  icon: i-simple-icons-github
  ---
  GitHub
  :::
::

::u-page-section
---
class: "max-w-none px-0"
---
  :::u-page-grid
  ---
  class: "grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"
  ---

    :::u-page-card
    ---
    spotlight: true

    class: "group col-span-1"
    ---
      :::floating-flutter
      :::

    #title
    Build to be [easy]{.text-primary}

    #description
    Built to be truly plug-and-play, this package focuses on [simplicity]{.text-primary} and [efficiency]{.text-primary} — configure a client, define your models, and start talking to your Laravel REST API.
    :::

    :::u-page-card
    ---
    spotlight: true

    class: "group col-span-1"
    ---
      :::floating-flutter
      ---
      image: "/shird_block.png"
      ---
      :::
    #title
    Highly [modular]{.text-primary}

    #description
    Designed to do [more with less]{.text-primary} — start simple, keep it light, and add only the repositories and endpoints you need. A minimal, modular foundation that [grows with your project]{.text-primary}.
    :::

    :::u-page-card
    ---
    spotlight: true

    class: "group col-span-1"
    ---
      :::floating-flutter
      ---
      image: "/shird_chest.png"
      ---
      :::

    #title
    A lot of [Compatibility]{.text-primary}

    #description
    Optimized for seamless integration with any Laravel REST API and your existing Flutter stack. Swap HTTP clients, adjust headers, or extend repositories without changing your UI.
    :::
  :::



  :::u-page-section
  ---
  ui:
    container: sm:py-6 lg:py-7 py-6
  title: First Steps
  id: first-steps
  ---
  :::

  :::u-page-section
  ---
  ui:
    container: sm:py-6 lg:py-7 py-6
  title: Installation Guide
  orientation: horizontal
  variant: naked
  ---
  #description
  Quick installation setup.
    :::prose-pre
    ---
    code: flutter pub add laravel_rest_api_flutter
    filename: Terminal
    ---
    ```bash
     flutter pub add laravel_rest_api_flutter
    ```
    :::

  #default
    :::prose-pre
    ---
    filename: pubspec.yaml
    ---
    ```yaml
    dependencies:
      flutter:
        sdk: flutter
      laravel_rest_api_flutter: any
      dio: any # or your preferred HTTP package
    ```
    :::
  :::
  :::u-page-section
  ---
  ui:
    container: sm:py-6 lg:py-2 py-6
  title: Minimal Setup
  orientation: horizontal
  variant: naked
  reverse: true
  ---
  #description
  Instantiate your API client and a simple repository.
    :::custom-prose-with-bird
    :::
    :::prose-pre
    ---
    filename: repository_usage.dart
    ---
    ```dart
    final repository = ItemRepository();

    Future<void> fetchItems() async {
      final response = await repository.search(
        filters: [
          Filter(field: 'name', type: 'contains', value: 'Test'),
        ],
      );

      if (response.isSuccessful) {
        print(response.body);
      } else {
        print('Error: ${response.statusCode}');
      }
    }
    ```
    :::

  #default
    :::prose-pre
    ---
    filename: api_client.dart
    ---
    ```dart
    class ApiHttpClient implements RestApiClient {
      final Dio dio;

      ApiHttpClient({required this.dio});

      @override
      Future<RestApiResponse> get(
        String url, {
        Map<String, String>? headers,
        Map<String, String>? queryParams,
      }) async {
        try {
          final response = await dio.get(
            '\${dio.options.baseUrl}\$url',
            options: Options(headers: headers),
            queryParameters: queryParams,
          );
          return RestApiResponse(
            statusCode: response.statusCode,
            body: response.data,
          );
        } catch (exception, stackTrace) {
          return handleError(exception, stackTrace);
        }
      }

      // post/delete implementations can follow the same pattern
    }
    ```
    :::
  :::


  :::u-page-section
  ---
  ui:
    container: sm:py-6 lg:py-7 py-6
  title: Mutations & Actions
  orientation: horizontal
  variant: naked
  ---
  #description
  Create or update records and trigger custom actions defined in your Laravel backend.
    :::prose-pre
    ---
    filename: mutations.dart
    ---
    ```dart
    final newItem = ItemModel(id: 3, name: 'New Item');

    await repository.mutate(
      body: LaravelRestApiMutateBody(
        mutate: [
          Mutation(
            operation: MutationOperation.create,
            attributes: newItem.toJson(),
          ),
          Mutation(
            operation: MutationOperation.update,
            key: 3,
            attributes: {'name': 'Updated Name'},
          ),
        ],
      ),
    );
    ```
    :::

  #default
    :::prose-pre
    ---
    filename: actions.dart
    ---
    ```dart
    await repository.actions(
      data: LaravelRestApiActionsBody(
        fields: [
          Action(name: 'expires_at', value: '2023-04-29'),
        ],
      ),
    );
    ```
    :::
  :::


  :::u-page-section
  ---
  ui:
    container: sm:py-6 lg:py-7 py-6
  ---
  #links
    :::u-button
    ---
    color: primary
    size: xl
    to: /getting-started/introduction
    trailingIcon: i-lucide-arrow-right
    ---
    Get started
    :::
  :::

  ::u-page-section
    :::like-section
    :::

  ::
::
