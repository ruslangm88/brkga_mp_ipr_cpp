.. index:: pair: namespace; BRKGA
.. _doxid-namespace_b_r_k_g_a:
.. _cid-brkga:

namespace BRKGA
===============

.. toctree::
	:hidden:

	namespace_BRKGA_PathRelinking.rst
	enum_BRKGA_BiasFunctionType.rst
	enum_BRKGA_Sense.rst
	enum_BRKGA_ShakingType.rst
	class_BRKGA_BRKGA_MP_IPR.rst
	class_BRKGA_BrkgaParams.rst
	class_BRKGA_DistanceFunctionBase.rst
	class_BRKGA_ExternalControlParams.rst
	class_BRKGA_HammingDistance.rst
	class_BRKGA_KendallTauDistance.rst
	class_BRKGA_Population.rst

Overview
~~~~~~~~

This namespace contains all stuff related to Multi-Parent BRKGA with Implicit Path Relinking. :ref:`More...<details-doxid-namespace_b_r_k_g_a>`


.. ref-code-block:: cpp
	:class: overview-code-block

	
	namespace BRKGA {

	// namespaces

	namespace :ref:`BRKGA::PathRelinking<doxid-namespace_b_r_k_g_a_1_1_path_relinking>`;

	// typedefs

	typedef std::vector<double> :ref:`Chromosome<doxid-namespace_b_r_k_g_a_1ac1d4eb0799f47b27004f711bdffeb1c4>`;

	// enums

	enum :ref:`BiasFunctionType<doxid-namespace_b_r_k_g_a_1af0ede0f2a7123e654a4e3176b5539fb1>`;
	enum :ref:`Sense<doxid-namespace_b_r_k_g_a_1af28538be111c8320b2fec44b77ec5e9b>`;
	enum :ref:`ShakingType<doxid-namespace_b_r_k_g_a_1a616e3d7dedad5ff4e6a2961cda1ea494>`;

	// classes

	template <class Decoder>
	class :ref:`BRKGA_MP_IPR<doxid-class_b_r_k_g_a_1_1_b_r_k_g_a___m_p___i_p_r>`;

	class :ref:`BrkgaParams<doxid-class_b_r_k_g_a_1_1_brkga_params>`;
	class :ref:`DistanceFunctionBase<doxid-class_b_r_k_g_a_1_1_distance_function_base>`;
	class :ref:`ExternalControlParams<doxid-class_b_r_k_g_a_1_1_external_control_params>`;
	class :ref:`HammingDistance<doxid-class_b_r_k_g_a_1_1_hamming_distance>`;
	class :ref:`KendallTauDistance<doxid-class_b_r_k_g_a_1_1_kendall_tau_distance>`;
	class :ref:`Population<doxid-class_b_r_k_g_a_1_1_population>`;

	// global functions

	:ref:`INLINE<doxid-brkga__mp__ipr_8hpp_1a2eb6f9e0395b47b8d5e3eeae4fe0c116>` std::pair<:ref:`BrkgaParams<doxid-class_b_r_k_g_a_1_1_brkga_params>`, :ref:`ExternalControlParams<doxid-class_b_r_k_g_a_1_1_external_control_params>`> :ref:`readConfiguration<doxid-namespace_b_r_k_g_a_1ad212f0711891038e623f4d882509897e>`(const std::string& filename);

	:ref:`INLINE<doxid-brkga__mp__ipr_8hpp_1a2eb6f9e0395b47b8d5e3eeae4fe0c116>` void :ref:`writeConfiguration<doxid-namespace_b_r_k_g_a_1a01bade43afee725ca73c3f45a76012c4>`(
		const std::string& filename,
		const :ref:`BrkgaParams<doxid-class_b_r_k_g_a_1_1_brkga_params>`& brkga_params,
		const :ref:`ExternalControlParams<doxid-class_b_r_k_g_a_1_1_external_control_params>`& control_params = :ref:`ExternalControlParams<doxid-class_b_r_k_g_a_1_1_external_control_params>`()
		);

	} // namespace BRKGA
.. _details-doxid-namespace_b_r_k_g_a:

Detailed Documentation
~~~~~~~~~~~~~~~~~~~~~~

This namespace contains all stuff related to :ref:`BRKGA <doxid-namespace_b_r_k_g_a>` Multi Parent with Implicit Path Relinking.

Typedefs
--------

.. index:: pair: typedef; Chromosome
.. _doxid-namespace_b_r_k_g_a_1ac1d4eb0799f47b27004f711bdffeb1c4:
.. _cid-brkga.chromosome:

.. ref-code-block:: cpp
	:class: title-code-block

	typedef std::vector<double> Chromosome

Chromosone representation.

The chromosome is represented using a vector in the unitary hypercube, i.e., :math:`v \in [0,1]^n` where :math:`n` is the size of the array (dimensions of the hypercube). We use double precision because float precision maybe not be enough for some applications.

We could use ``std::vector<double>`` directly. However, using typedef, we can add additional capabilities to the Chromosome class in the future, such as parenting track. For example, we may want to do this:

.. ref-code-block:: cpp

	class :ref:`Chromosome <doxid-namespace_b_r_k_g_a_1ac1d4eb0799f47b27004f711bdffeb1c4>`: public std::vector<double> {
	    public:
	        :ref:`Chromosome <doxid-namespace_b_r_k_g_a_1ac1d4eb0799f47b27004f711bdffeb1c4>`() :
	            :ref:`std <doxid-namespacestd>`::vector<double>(), my_personal_data(0.0)
	            {}
	    public:
	        double my_personal_data;
	};

to keep track of some data within a specifc chromosome.

In general, most people do not recommend to inherit publicly from ``std::vector<>`` because it has no virtual destructor. However, we may do that as long as:

a) We remember that every operation provided by ``std::vector<>`` must be a semantically valid operation on an object of the derived class;

b) We avoid creating derived class objects with dynamic storage duration;

c) We **DO AVOID** polymorphism:

.. ref-code-block:: cpp

	std::vector<double>* pt = new :ref:`Chromosome <doxid-namespace_b_r_k_g_a_1ac1d4eb0799f47b27004f711bdffeb1c4>`();     // Bad idea
	delete pt;      // Delete does not call the Chromosome destructor

Global Functions
----------------

.. index:: pair: function; readConfiguration
.. _doxid-namespace_b_r_k_g_a_1ad212f0711891038e623f4d882509897e:
.. _cid-brkga.readconfiguration:

.. ref-code-block:: cpp
	:class: title-code-block

	:ref:`INLINE<doxid-brkga__mp__ipr_8hpp_1a2eb6f9e0395b47b8d5e3eeae4fe0c116>` std::pair<:ref:`BrkgaParams<doxid-class_b_r_k_g_a_1_1_brkga_params>`, :ref:`ExternalControlParams<doxid-class_b_r_k_g_a_1_1_external_control_params>`> readConfiguration(const std::string& filename)

Reads the parameters from a configuration file.

.. todo::
  (ceandrade) This method can beneficiate from introspection tools from C++17.
  We would like achieve a code similar to the `Julia counterpart
  <https://github.com/ceandrade/brkga_mp_ipr_julia>`_.

.. rubric:: Parameters:

.. list-table::
	:widths: 20 80

	*
		- filename

		- the configuration file.


.. rubric:: Returns:

a tuple containing the :ref:`BRKGA <doxid-namespace_b_r_k_g_a>` and external control parameters.

.. rubric:: Exceptions:

.. list-table::
	:widths: 20 80
    
	*
		- std::fstream::failure

		- in case of errors in the file.


.. index:: pair: function; writeConfiguration
.. _doxid-namespace_b_r_k_g_a_1a01bade43afee725ca73c3f45a76012c4:
.. _cid-brkga.writeconfiguration:

.. ref-code-block:: cpp
	:class: title-code-block

	:ref:`INLINE<doxid-brkga__mp__ipr_8hpp_1a2eb6f9e0395b47b8d5e3eeae4fe0c116>` void writeConfiguration(
		const std::string& filename,
		const :ref:`BrkgaParams<doxid-class_b_r_k_g_a_1_1_brkga_params>`& brkga_params,
		const :ref:`ExternalControlParams<doxid-class_b_r_k_g_a_1_1_external_control_params>`& control_params = :ref:`ExternalControlParams<doxid-class_b_r_k_g_a_1_1_external_control_params>`()
		)

Writes the parameters into a file.

.. todo::
  (ceandrade) This method can beneficiate from introspection tools from C++17.
  We would like achieve a code similar to the `Julia counterpart
  <https://github.com/ceandrade/brkga_mp_ipr_julia>`_.

.. rubric:: Parameters:

.. list-table::
	:widths: 20 80

	*
		- filename

		- the configuration file.

	*
		- brkga_params

		- the :ref:`BRKGA <doxid-namespace_b_r_k_g_a>` parameters.

	*
		- control_params

		- the external control parameters. Default is an empty object.

.. rubric:: Exceptions:

.. list-table::
	:widths: 20 80
    
	*
		- std::fstream::failure

		- in case of errors in the file.
